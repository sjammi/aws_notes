## Aurora
- Proprietary
- supports Postgres + MySQL drivers
- More expensive, "more efficient"
- High availability and high reads scaling
- Only master writes, in case of failover another is chosen

- Can define custom endpoints to point to specific instances (say, the 4x's instead of 2x's for analytics)

---

## Types
- Serverless
  - automated instantiation and scaling by usage
  - pay per second
  - infrequest or unpredictable workloads
- Multi-Master
  - Handles immediate failovers
  - Every node handles Read/Write
- Global
  - Cross Region RR: disaster recovery, easy
  - Global DB: 1 primary read/write region, RRs in up to 5 other regions
  - ## 1 second cross region replication

---

## Machine Learning
- Add predictions via SQL
- Integrates with AWS ML
  - uses Sagemaker, Comprehend, etc

---

## Backups
- Automated
  - Daily backups
  - Logs backed up every 5 min
  - deletes after retention
- Manual
  - no default delete


## DB Cloning
- make new cluster from existing
- faster than snapshot
- 

