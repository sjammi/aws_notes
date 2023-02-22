## EFS (Elastic File System)
- Managed NFS (network)
- works across AZs
- highly available, scalable, $$$$$$$
  - content management, web serving, data sharing
- NFSv4.1 protocol
- uses Security group
- Linux only
- Size scales automatically, pay per use

---

## Performance & Storage Class
- Performance mode:
  - general (latency sensitive)
  - ## max I/O: higher latency, throughput, highly parallel (big data, media processing)

- Throughput Mode:
  - ## much much faster (5x, 10x burst)
  - Speed set regardless of size
  - Elastic: scales throughput based on use
  
- Storage Classes:
  - c h e a p
  - tiers:
    - standard: files you use
    - (EFS-IA) infrequent: cost to get, cheaper to store
  - Availability:
    - standard: multi AZ
    - one zone: uno AZ
  - 



