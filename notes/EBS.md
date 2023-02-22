## EBS (Elastic Block Store) Volume
- *network drive*
- can persist data after termination
- 1 instance mount at a time
- bound to AZ
- 30GB free, then per month
- provisioned capacity
- Delete on termination option
- Can take snapshot to archive / share
- can delete / has retention policies
- $$$$$ for fast restore

---

## Volume Types
- SSD:
  - gp2/3: balanced
    - cheap, low latency
    - 1gb - 16tb
    - 2
      - 3 IOPS per GB
      - Volume size / IOPS linked (up to 16K)
    - 3
      - baseline 3k IOPS and 125 mb/s
  - io1/2: high performance for low latency + high throughput
    - need very high speed
    - great for DBs
    - ## for very high IOPS (16K+)
    - ## can increase PIOPS[^1] separately from storage size
    - Supports multi-attach (EBS)
    - block express for that extra extra speed
- HDD:
  - 125gb-16tb
  - st1: frequent access and high throughput
    - big data, warehouses, log processing
    - 500 mb/s, max IOPS 500
  - sc1: cheapest
    - infrequent use, lowest cost
    - 500 mb/s, max IOPS 250

- ## SSDs only for boot volumes

---

## Multi-attach
- 1 EBS -> several EC2 instances (same AZ)
- ## Higher application availability
  - must manage concurrent writes
- 16 instances max

---

## Encryption
- Gets you:
  - data at rest is encrypted
  - data in flight instance <-> volume encrypted
  - snapshots encrypted
  - volumes built from snapshot
- handled transparently, minimal latency effect, uses keys from [KMS](../KMS.md)
- snapshots are encrypted, and unencrypted snapshots can be encrypted
  



[^1]: PIOPS: Provisioned IOPS