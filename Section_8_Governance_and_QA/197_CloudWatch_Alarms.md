# 197. CloudWatch Alarms

Alarms **trigger actions or notifications from a metric**, using statistics such as sampling, percentage or maximum.

## States and period

| State | Meaning |
|---|---|
| `OK` | Not triggered |
| `INSUFFICIENT_DATA` | Not enough data to decide |
| `ALARM` | Threshold breached |

The **period** is the time over which the metric is evaluated. For **high-resolution custom metrics** it can be **10 s, 30 s or a multiple of 60 s**.

## Targets

| Target | Actions |
|---|---|
| **EC2 instance** | Stop, terminate, reboot, **recover** |
| **Auto Scaling** | Scale out or in |
| **SNS** | Notify, and from there run **Lambda** to do almost anything |

## Composite alarms

- A normal alarm watches **one metric**; a **composite alarm** watches the **states of other alarms**.
- Combine them with **AND** / **OR**.
- Used to **reduce alarm noise**, for example alert only when CPU is high **and** network is low.
- Example: Alarm A (CPU) **AND** Alarm B (IOPS) → composite alarm → SNS.

## EC2 instance recovery

| Status check | Checks |
|---|---|
| **Instance** | The virtual machine |
| **System** | The underlying hardware |
| **Attached EBS** | Health of attached volumes |

- An alarm on a status check can start **recovery**, which moves the instance to another host. In AWS the recover action is tied to the **system** status check.
- Recovery keeps the **private, public and Elastic IP**, **metadata** and **placement group**.
- An **SNS** notification can announce it.

## Logs and testing

- **Metric filter → alarm → SNS**, for example when the word `error` appears too often.
- Test an alarm's actions without breaching the threshold: CLI **`set-alarm-state`**.

## Exam takeaways

1. Several conditions → **composite alarm**.
2. Hardware problem → **alarm + EC2 recovery** (same IPs, metadata, placement group).
3. Test an alarm → **`set-alarm-state`**.
