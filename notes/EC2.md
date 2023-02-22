## Overall
- Elastic Cloud Compute
- IaaS -> Infra as a service
- Accomplishes:
  - renting VMs (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines (ELB)
  - Scaling services using an auto-scaling group (ASG)

---

## Sizing and Config
- AMI (OS)
- Size (CPU, RAM)
- Storage
  - network store (EBS / EFS)
  - hardware (EC2 instance store)
- Security Group (Firewall Rules)
- Bootstrap script
- Network Card
- Instance Role:
  - [IAM](IAM.md)

m5.2xlarge  
-> m: instance class  
-> 5: generation  
-> 2xlarge: size in instance class  

"General Purpose":  
- Balance between compute / memory / networking  
- M's, T's, A1  

"Compute Optimized":
- high performance
- batch processing, media transcoding, compute/server, ML, gaming
- C's  

"Memory Optimized":
- high performance DBs, cache store, in memory DB (for BI use) 
- R's, X's, Z1

"Storage Optimized":
- online transaction processing, relational / nosql dbs, cache for in-memory (ex Redis), data warehousing 
- I's, D's, H1

---

## Security Groups
- Fire wall
- Controls traffic in/out of EC2
- "allow" rules only
- reference by IP or Group
- reusable
- region locked
- external to EC2
- *make a separate one for SSH access*

Regulates:
  - ports
  - ip ranges
  - controls inbound/outbound network
  
- Inbound blocked by default
- Outbound open by default

Classic ports:
  - 22: SSH / SFTP
  - 21: FTP
  - 80: HTTP
  - 443: HTTPS
  - 3389: RDP (Remote Desktop Protocol for Win)


---

## Purchase Options
On-demand:
  - short workload, pay by second
  - Highest cost but not upfront
  - good for un-interrupted work

Reserved:
  - 1-3 years
    - much cheaper for 1, much much for 3
  - Pay options over time or up front
  - Reserved instances
    - edit type, region, tenacity[^1], OS
  - Convertible reserved instances (more flexible)
    - edit type, instance family, OS, "scope?", tenacity[^1]  
  - Scope: Regional or Zonal

Savings Plans:
  - Commitment to amount of use
  - discount for long term usage
  - certain type of usage ($10/hour for 1 or 3 years)
  - On demand price if extended
  - Instance family and region locked

Spot instances:
  - short, cheap, can lose instances
  - "lose" any time if acc max price < current spot price
  - *good for resilient workloads:*
    - batch jobs
    - data analysis
    - image processing
    - distributed work
    - flexible start/end
  - PROCESS:
    - define max price, stop/terminate with grace period
    - "Spot Block" instance during time period

Dedicated hosts:
  - book entire physical server
  - allows compliance requirements + server bound software licenses
  - On demand or reserved
  - $$$$$$$$$$$
  - ## for strong regulatory needs

Dedicated instances:
  - only for me, no other customers
  - Dedicated Hosts but with more specific billing and nothing else

Capacity reservations:
  - reserve in specific AZ[^2] for any length
  - no time commitment, no billing discounts
  - Charged on-demand whether running or not

Spot Fleets:
  - set of spot and on demand instances
  - tries to meet capacity within price constraints
  - Strategies:
    - lowestPrice: from pool with lowest price (cost optimization, short workload)  
• diversified: distributed across all pools (availability, long workloads)  
• capacityOptimized: optimal capacity for # of instances  

---

## IP
- IPv4
  - ###.###.###.###
  - 3.7 billion possible addresses
- IPv6
  - 3ffe:1900:4545:3:200:f8ff:fe21:67cf
  - better but we ain't there yet
- Public v Private:
  - public:
    - identifiable on internet
    - must be unique
    - can be geo-located
  - private:
    - identifiable on private network only
    - unique on network
    - connect using NAT + gateway
    - specific range of IPs
- Elastic IPs
  - EC2 instance changes IP on start/stop
  - Elastic allows for a fixed IP
  - Allows for remapping address in case of failure
  - 5 per account by default
  - Pretty cringe to use bro
  - Load Balancer all the way

---

## Placement Groups
- To control instance placement
- Strategies:
  - Cluster: cluster in low latency group in an AZ[^2]
  - Spread: across underlying hardware (7 instances per group per AZ[^2])
  - Partition: spread across many different partitions within AZ[^2]. Up to 100s per group (hadoop, cassandra, kafka, etc)

- PG Cluster:
  - great network
  - rack fails then all fail
  - low latency and high network throughput

- Groups spread:
  - Spans AZs, on different physical hardware, reducing simul fail risk
  - 7 instances per AZ per PG
  - *Max high availability, needs fail-safe isolated instances*

- Groups Partition:
  - 7 Partitions per AZ
  - Spans multiple AZs
  - Does not share racks with other partition instances
  - EC2 instances get partition info as metadata
  - HDFS, HBase, Cassandra, Kafka

- ENI (Elastic Network Interfaces)
  - represents Virtual Network Card
  - Primary and secondary private IPv4s, one Elastic IP, one Public IP, security groups, MAC address
  - Create independently and attach to instances
  - Bound to AZ

---

## Hibernate
- stop v terminate:
  - stop keeps disk intact
- start:
  - OS boots  
  - bootstrap run (only on first start)
  - app start
  - cache warms up
- Hibernate preserves in-memory state
  - speeds up boot
  - RAM written to file in EBS volume (MUST be encrypted)
- Good for long running processes and slow to start services
- Requirements:
  - supports C, I, M, R, T instance families
  - > 150GB
  - No bare metal instance sizes
  - AMI - linux or win
  - Root volume - EBS and encrypted
  - on demand, reserved, or spot instances
- *MAX 60 days*

---

## Storage Selection
- [EBS](./sub_notes/EBS.md)
- [EFS](./sub_notes/EFS.md)
- EBS vs EFS:
  - EBS:
    - one instance
    - locked by AZ
    - gp2: IO increases with disk
    - io1: IO increases independently
    - backups take IO bandwidth
    - terminates by default
  - EFS:
    - Many instances
    - Share site files
    - linux only
    - more $$$$
    - EFS-IA if valuable
- Instance Store
  - better I/O
  - Ephemeral, loses data if stopped
  - Good for cache / temp content
  - Risk data loss, backup on user

---

## AMI (Amazon Machine Image)
- customization of EC2 instance
  - software, config, OS, monitoring, etc
  - faster boot cause packaged
- Built for a region
- Launch from:
  - public AMI
  - own AMI
  - marketplace AMI
- To make:
  - Start instance
  - customize
  - stop (NOT terminate)
  - "Build an AMI", also creates EBS snapshots
  - use elsewhere



### Footnotes
[^1]: Tenacity - host, dedicated, default  
[^2]: AZ - Availability Zone  