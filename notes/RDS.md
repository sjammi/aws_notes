## Options
- PG
- MySQL
- MariaDB
- Oracle
- Msft SQL Server
- Aurora
  
Cannot SSH in, but nice  

Read replicas are nice
- for, say reporting
- or constant writes
- its a read replica, you know this part
- Free in same region

---

## Security
- at rest encryption
  - encryption using KMS - must be defined at launch
  - if master has enc, so can RR
  - snapshot and restore to add enc
- in flight: TLS by default
- IAM
- Security Groups
- ## no SSH except RDS Custom

---

## Proxy
- fully managed
- apps can share DB connections
- minimize failover time
- adds IAM auth
- never publicly accessible


