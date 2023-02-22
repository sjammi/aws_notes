## Exam 1 Results
- dynamodb  
  - DAX: in memory cache
- S3 Lifecycle  
- S3 tiers  
- Glacier
- API Gateway  
- Cloudfront  
  - CDN (Content Delivery Network) - handles static / dynamic content sending
  - CF using regional caches greatly increases send speed.
- Inspector
- Guard Duty  
    - Disabling deletes all data
- Kinesis  
- Neptune?  
  - Graph shit
- Snowmobile? Snowball?  
  - Data transfer utilities
  - Snowball: under 10PB
  - Snowmobile: over 10PB
- Cost order stuff  
- Fargate
  - Serverless containers
  - EC2 or EKS
  - Create tasks and they run
- FSx
  - persistent or temp
  - Couple types
    - Windows
      - say, migrate off Win hardware
    - Lustre
      - HPC
    - Netapp
      - Cheap, spin up lots of space
    - Openzfs
      - cheap, spin up s p e e d
  - Virtual storage, fast af


Missed:
- What are valid transitions in an S3 lifecycle
  - Any storage -> Glacier / Glacier deep
  - Standard-IA -> Intelligent tiering OR One Zone-IA
  - Intelligent-tiering -> One Zone-IA
  - Glacier -> Glacier deep

- Using GuardDuty, all findings have to be deleted
  - Disabling Guard Duty deletes all data

- User deleted Customer Master Key yesterday, what do
  - If CMK is deleted, pends for a day and cancellable
  - After, all gone get customer support

- Sharing EFS file around world
  - Add an inter-region VPC connection

- Replication strategy in RDS (Multi AZ and RR)
  - Multi-AZ uses synchronous replication
  - RRs use asyncronous replication

- S3 bucket retention safety policy
    - On OBJECT [**NOT bucket**] level, specify `Retain Until Date` and use object versions

- S3 + S3TA file upload charges
  - S3 upload is free
  - S3TA charges by measurable speed boost (free if it didn't help)

- Thousands of hardware devices need real time analytics
  - Kinesis Data Streams

- Need maintanence on EC2 cluster, ASG messing things up
  - Set instance to standby
  - suspend ReplaceUnhealthy

- API Gateway - stateful or stateless?
  - RESTful APIs are stateless
  - WebSocket APIs are stateful

- What bypasses the Cloudfront regional edge cache?
  - proxy methods
  - dynamic content

- Need better S3 file upload speed
  - S3TA
  - Multipart uploads

- Protect S3 data and check EC2 for vulns
  - GuardDuty to monitor S3
  - Inspector to do security checks

- Need temporary storage and random high I/O perf
  - Instance Store for physical distance and temp data

- Need to handle and store game updates
  - Kinesis DS -> Lambda for real time ingest

- Want faster speeds globally, UDP protocol, custom DNS
  - Global Accel for world, ELB is regional

- Want faster dynamodb
  - DAX
  - Elasticache for other caching cases

- What S3 bucket feature can only be suspended after enable
  - versioning

- Need throttling/buffering
  - API Gateway, SQS, or Kinesis

- What kind of EC2 instances to use for prod with dev clones during work hours
  - Reserved for prod (duh)
  - on-demand for dev
    - spot instances would work, but time limit too short

- One Zone IA usage
  - Can only be moved to one zone after 30 days

- Sensor service, want serverless and no manual handling
  - SQS -> Lambda -> Dynamo
  - NOT Firehose - doesn't write to Dynamo

- In memory data store, on demand live needs
  - DynamoDB + DAX
  - Redis

- Company has legacy DBs with custom config, what do
  - Use RDS Custom

- Most cost effective for an S3 file, needed for 24 hours after storage
  - Standard S3

- Move tons of data
  - Snowball (< 10PB) + Site to Site VPN

- ECS + EC2 vs ECS + Fargate pricing
  - EC2 - charge based on instances and volumes used
  - Fargate - charge based on vCPI and mem requested

- Filter out site traffic from other countries
  - Use Cloudfront

- Need secure data from customer in S3 with Encryption audit log
  - Secure using KMS

- Terabytes of data, accessed 2x a year, need fast latency
  - S3 Standard-IA, Infrequent Access still fast af

- Cost of storing on S3 standard vs EBS vs EFS
  - S3 -> EFS -> EBS
  - EFS pay by space used
  - EBS pay by block of storage

- Data process needs 60 min and can stop/start, optimize for cost
  - Use EC2 spot instance
  - way cheaper than on demand

- Using SNS and Lambda, system is having failures from too many requests
  - 5K requests per second, too many for SNS -> Lambda

- Lots of data, need to split into hot and cold data
  - FSx Lustre - good for high performance computing, allows writes to S3 as files

- Process that can handle up to 1K messages per second
  - SQS with FIFO
  - Process messages in batches of 4 because FIFO supports up to 300/s, 4 brings it past 1K

- Complaince and regulatory guidelines for S3 store
  - Enable MFA delete, enable versioning







