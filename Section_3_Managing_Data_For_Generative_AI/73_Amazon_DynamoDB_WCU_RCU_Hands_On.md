# 73. Amazon DynamoDB - WCU & RCU - Hands On

Changing the capacity mode of a table in the console, using the **capacity calculator**, and setting up **auto scaling** for a provisioned table.

## Steps

1. Open the `Users` table, choose **Additional settings** on the right and edit **Read/Write capacity**. This is the setting chosen at creation, and it can be changed at any time, including switching modes.
2. **On-demand** gives simplified billing for the actual reads and writes. It is two to three times as expensive as provisioned, so it fits unpredictable workloads or a development table that sits unused for most of the day and is hit hard for an hour.
3. **Provisioned** is the mode to understand in depth. Open the **capacity calculator** and enter an average item size (for example 6 KB), reads per second (3), writes per second (2), the read type and the write type.
4. The calculator returns the **RCU, WCU and estimated cost** for those inputs.
5. Back on the table, auto scaling can be **off** for reads and writes, which fixes the provisioned units until they are changed by hand, or **on**.
6. Turn auto scaling on for both reads and writes with a minimum of 1 and a maximum of 3, then save.
7. After a short wait, **Auto scaling activities** shows reads and writes lowered to 1, because the table is not being used. The table now shows 1 RCU and 1 WCU, down from 2 and 2.

## Settings that mattered

| Setting | Notes |
| --- | --- |
| Read type in the calculator | **Eventually consistent** or **strongly consistent**. A **transactional** option exists and is covered later |
| Write type in the calculator | **Standard** or **transactional**, also covered later |
| Auto scaling minimum and maximum | The range DynamoDB may scale within |
| Target utilisation | A percentage. DynamoDB adjusts capacity to keep consumption near it |

## What the demo showed

- Capacity mode and capacity units can be **changed after table creation**.
- Auto scaling needs only a **minimum, a maximum and a target utilisation**. For a maximum of 100 and about 70 consumed units, capacity is set near 100. With only 7 consumed, desired capacity drops to 10.
- It applies to reads and writes separately and behaves like EC2 auto scaling, but for DynamoDB.

## Exam takeaways

1. Practise the **capacity calculator**. The exam asks you to work out RCU and WCU for given item sizes and rates.
2. Auto scaling takes a min, a max and a target utilisation, so you do not size capacity by hand.
3. On-demand suits unpredictable or sporadic use. Provisioned suits steady, predictable traffic and is cheaper.
