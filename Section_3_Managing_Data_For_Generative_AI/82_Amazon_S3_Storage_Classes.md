# 82. Amazon S3 - Storage Classes

The **S3 storage classes**, how durability and availability differ between them, and how to pick one.

## Overview

- Classes: **Standard**, **Standard-IA**, **One Zone-IA**, **Glacier Instant Retrieval**, **Glacier Flexible Retrieval**, **Glacier Deep Archive** and **Intelligent-Tiering**.
- You choose the class when you create an object, and can change it manually later or move objects automatically with **S3 Lifecycle configurations**.
- You need to know these classes for the exam.

## Durability and availability

- **Durability** is how likely S3 is to lose an object. It is **99.999999999% (11 nines)** across multiple AZs and is the **same for all storage classes**. Storing 10,000,000 objects means losing one on average once every 10,000 years.
- **Availability** is how readily the service can be used, and **varies by class**. Standard has 99.99%, which is about **53 minutes a year** of unavailability, so applications must handle errors.

## The classes

| Class | Availability | Min storage duration | Min billable size | Retrieval | Use case |
| --- | --- | --- | --- | --- | --- |
| **Standard** | 99.99% | None | None | No fee, low latency, high throughput | Big data analytics, mobile and gaming apps, content distribution |
| **Intelligent-Tiering** | 99.9% | None | None | No retrieval charges, small monthly monitoring and auto-tiering fee | Unknown or changing access patterns |
| **Standard-IA** | 99.9% | 30 days | 128 KB | Per GB retrieved | Disaster recovery, backups |
| **One Zone-IA** | 99.5% | 30 days | 128 KB | Per GB retrieved | Secondary backup copies of on-premises data, data you can recreate |
| **Glacier Instant Retrieval** | 99.9% | 90 days | 128 KB | Milliseconds, per GB retrieved | Archive accessed about once a quarter |
| **Glacier Flexible Retrieval** | 99.99% | 90 days | 40 KB | Expedited 1 to 5 minutes, Standard 3 to 5 hours, Bulk 5 to 12 hours (free) | Archive and backup |
| **Glacier Deep Archive** | 99.99% | 180 days | 40 KB | Standard 12 hours, Bulk 48 hours | Long-term storage at the lowest cost |

- **Standard** sustains **2 concurrent facility failures**.
- **Standard-IA** and **One Zone-IA** are for data accessed less often but needed rapidly, at a lower storage cost than Standard plus a retrieval cost.
- **One Zone-IA** keeps data in a **single AZ** (other classes use 3 or more), so data is lost if the AZ is destroyed.
- **Glacier** classes are low-cost archive storage, priced as storage plus retrieval cost.
- **Glacier Flexible Retrieval** was formerly called Amazon S3 Glacier.
- Instant means retrieved immediately, flexible means you can wait minutes to hours.

## Intelligent-Tiering tiers

| Tier | Type | Objects move here when |
| --- | --- | --- |
| Frequent Access | Automatic, default | Default |
| Infrequent Access | Automatic | Not accessed for **30 days** |
| Archive Instant Access | Automatic | Not accessed for **90 days** |
| Archive Access | Optional | Configurable from **90 to 700+ days** |
| Deep Archive Access | Optional | Configurable from **180 to 700+ days** |

## Exam takeaways

1. Durability is **11 nines for every class**. Only availability, minimum duration, minimum size and retrieval cost differ.
2. **One Zone-IA** is for recreatable data or secondary copies, as it lives in one AZ.
3. Glacier minimum durations: **90 days** (Instant and Flexible) and **180 days** (Deep Archive). Deep Archive retrieval takes 12 hours (Standard) or 48 hours (Bulk).
4. Use **Intelligent-Tiering** when access patterns are unknown. It has no retrieval charges.
