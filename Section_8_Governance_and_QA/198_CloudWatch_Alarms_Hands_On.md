# 198. CloudWatch Alarms - Hands On

Goal: **terminate an EC2 instance** when its CPU stays very high.

## Create the alarm

1. Launch a `t2.micro` instance and wait (about 5 minutes) for its metrics.
2. Select the **per-instance** metric **CPUUtilization**.
3. Statistic (average, sum, maximum and so on); **period 5 minutes**, as basic monitoring publishes every 5 minutes without **detailed monitoring**.
4. Condition: **static** threshold or **anomaly detection**. Demo: **greater than 95%**, **3 out of 3** datapoints (15 minutes).
5. Action: notification, Auto Scaling, **EC2 action** or Systems Manager. Demo: **terminate**.

The new alarm starts in **`INSUFFICIENT_DATA`**.

## Test it

Instead of loading the CPU for 15 minutes, set the state by hand:

```bash
aws cloudwatch set-alarm-state \
  --alarm-name <alarm-name> \
  --state-value ALARM \
  --state-reason "testing"
```

The alarm goes to **`ALARM`**, its **history** shows the change and the successful action, and the instance **terminates**.

## Exam takeaways

1. **`set-alarm-state`** runs the real actions, so test with care.
2. Basic EC2 monitoring is **5 minutes**; detailed monitoring is faster.
