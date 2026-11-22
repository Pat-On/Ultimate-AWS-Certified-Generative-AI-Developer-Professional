# 72. Amazon DynamoDB - WCU & RCU

How DynamoDB capacity works: the two capacity modes, how to compute **WCU** and **RCU**, consistency of reads, how capacity spreads across partitions, and what to do when requests are throttled.

## Capacity modes

| | Provisioned | On-demand (default) |
| --- | --- | --- |
| How it works | You specify RCU and WCU (reads and writes per second) in advance | Reads and writes scale up and down automatically with the workload |
| Planning | Required, auto scaling optional | None |
| Billing | Pay for what you provision, every hour | Pay for what you use, in **RRU** and **WRU** |
| Cost | Cheaper | About **2.5 times** more expensive |
| Use case | Predictable workloads | Unknown workloads, unpredictable traffic |

- You can switch between modes **once every 24 hours**.
- On-demand has unlimited capacity and **no throttling**. Every request succeeds, and RRU and WRU are computed like RCU and WCU, per request.

## Provisioned mode

- **RCU** is throughput for reads, **WCU** is throughput for writes.
- Auto scaling can adjust throughput to demand from a target utilisation.
- Exceeding the provisioned throughput first uses **burst capacity**. Once that is used up, DynamoDB raises **`ProvisionedThroughputExceededException`**, and the answer is a retry with **exponential backoff**.

## Computing WCU

- **1 WCU** is one write per second for an item up to **1 KB**. Larger items use more WCU, with the size **rounded up to the next KB**.
- Formula: writes per second × item size in KB (rounded up).

| Workload | Calculation | Result |
| --- | --- | --- |
| 10 items per second, 2 KB | 10 × 2 | **20 WCU** |
| 6 items per second, 4.5 KB | 6 × 5 | **30 WCU** (4.5 KB rounds up to 5 KB) |
| 120 items per **minute**, 2 KB | (120 / 60) × 2 | **4 WCU** (convert to per second first) |

## Strongly versus eventually consistent reads

- Data is replicated across servers, so a read may hit a replica that has not caught up yet.
- **Eventually consistent** is the default. A read right after a write can return stale data, as replication takes around 100 ms.
- **Strongly consistent** guarantees the latest data. Set `ConsistentRead = true` in **GetItem, BatchGetItem, Query and Scan**. It costs **twice the RCU** and has slightly higher latency, so use it only when needed.

## Computing RCU

- **1 RCU** is one **strongly consistent** read per second, or **two eventually consistent** reads per second, for an item up to **4 KB**. The size is **rounded up to the next multiple of 4 KB**.

| Workload | Calculation | Result |
| --- | --- | --- |
| 10 strongly consistent reads per second, 4 KB | 10 × (4 / 4) | **10 RCU** |
| 16 eventually consistent reads per second, 12 KB | (16 / 2) × (12 / 4) | **24 RCU** |
| 10 strongly consistent reads per second, 6 KB | 10 × (8 / 4) | **20 RCU** (6 KB rounds up to 8 KB) |

## Partitions and throttling

- A table is split into **partitions**, and the partition key goes through a hash function to choose one. The partition count formula (based on RCU, WCU and size) is not needed for the exam.
- Provisioned RCU and WCU are **spread evenly across partitions**. With 10 partitions and 10 WCU and 10 RCU, each partition gets 1 WCU and 1 RCU.
- Throttling happens when a partition exceeds its share. Typical causes are **hot keys** (one popular item read too often), **hot partitions** and **very large items**.
- Fixes:
  1. **Exponential backoff** (already built into the SDK).
  2. **Distribute partition keys** as widely as possible.
  3. For read problems, use **DynamoDB Accelerator (DAX)**, an in-memory cache covered later.

## Exam takeaways

1. Know the formulas and the rounding rules: **WCU rounds up to 1 KB, RCU rounds up to 4 KB** (6 KB counts as 8 KB).
2. Strongly consistent reads cost **double**. Eventually consistent is the default, with 1 RCU giving two reads per second.
3. Convert rates given per minute to per second before computing.
4. Burst capacity, then `ProvisionedThroughputExceededException`, then **exponential backoff**.
5. Throttling is **per partition**. Fix hot keys with better partition key design and read hot spots with **DAX**.
6. On-demand is the default, about 2.5 times the cost, never throttles and is billed in RRU and WRU. Modes can be switched once per 24 hours.
