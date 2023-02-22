## Elasticache
- # to manage redis or memcached
- high perf, low latency, great for read intensive
- stateless
- ## Lots of code changes
- ## Ex good for User Session storage

---

## Redis vs Memcached
- Redis
  - Multi AZ
  - RR's to scale
  - Data durability
  - Backup and restore
- Memcached
  - Shards - multiple nodes with partitioned data
  - Not highly available
  - Not persistent
  - No backup/restore
  - Multi threaded

---

## Security
- redis
  - IAM auth at API level
  - password/token on creation
  - SSL in flight
- Memcached
  - SASL based auth

---

## Patterns
- Lazy loading
  - all read data cached, can become stale
- Write through
  - Update cache on DB writes
- Session store
  - .... store.... session




