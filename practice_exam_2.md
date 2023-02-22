## Exam 2 Results

To review:
- default termination order:
  - allocation strat for on demand vs spot
  - oldest launch config
  - oldest launch template
  - closest to billing
- reserved or on demand for cost?
  - on demand more expensive
- Access Control Lists
- Amazon Cognito
  - Add user signup and auth
  - can be used to generate temp creds
  - User pools:
    - sign in functionality
    - Integrates with API Gateway and ALB
  - Identity pools:
    - AWS creds for users
  - vs IAM:
    - lots of users, mobile, SAML
- Credential management
  - ACM and Secret Manager creds automatically get renewed
  - days to expiry + cloudwatch would work, but why bother
- Security Groups -> stateful
- ACLs -> stateless
- Transit Gateway
    - Customer -> VPC, can interconnect VPCs as well
- VPC Peering
  - Connects 2 VPCs
- Private Link
  - For vv private connection
- when to use redshift
  - Redshift: data warehouse for storage and analysis

SCP:
- Service Control Policy
- Central control over permissions
- Have to have all features enabled
- Attached at organization level


Missed:
- Connect Multiple AWS accounts
  - shared services VPC (central source loc)

- Snowball to long time archive
  - snowball cannot write straight to glacier
  - snowball -> s3 -> glacier

- ETL Hadoop workload to cloud, highly available, 50 instances per AZ
  - Partition based
  - Spread is too small scale for Hadoop

- Improve Big data processing perf
  - boost Max I/O

- Single tenant hardware, regulatory guidlines, cost effective
  - Dedicated instances
  - Hosts would work but more expensive cause more visibility and control

- Limit access for devs in AWS
  - IAM permission boundaries only for role/user, not groups

- blue green deploy, global, handle DNS caching
  - Use Global Accelerator
  - R53 does DNS caching

- Handle permissions on user and account level in S3
  - S3 Bucket policies
  - Security Groups are firewalls for EC2

- Store less frequently accessed, concurrent access from hundreds of systems
  - EFS over S3
    - More specific to compute

- datasync for video files to EFS
  - Datasync - moves lots of data
  - for private conn VPC -> EFS, create interface VPC endpoint
    - or Direct Connect, or VPN, or peering
  - PrivateLink interface

- Need FIFO and a queue, scalable
  - Use SQS, needs a group ID to ensure order over multiple consumers
  - Kinesis would work but not well

- Need more availability in another region
  - latency based more practical than geolocation

- real time analytics. Data -> Kinesis DS -> K FH -> K Agent. Issue from DS to FH
  - Kinesis agent: standalone to send to DS or FH
  - FH and DS require different input from Agent, so must write into DS instead of FH first

- Need beefier system
  - spread across AZs
  - Cannot use ELB across regions

- Backups to cloud, data needs to be available to external vendors, lowest downtime
  - Cloudfront takes too long, requires downtime

- Multiple accts in a region, EC2s communicate privately. Cheapest
  - VPC in one account, share subnets using Resource Access Manager
  - Peering conn only for 1:1

- Decouple auth from app
  - Cognito + User Pools

- NFS for Linux, frequent at first then not
  - EFS is $ optimized for usage
  - No NFS in S3

- need 4 min EC2 instances
  - 2 per 3 AZs
    - that way its always over 4 with failovers

- key-value store with minute updates
  - Lambda + Dyanamo

- Cost optimization for EC2 using instance types
  - Multiple types can be defined in a Launch Template

- Unhealthy instance not dying
  - check has failed health check
  - check health check grace period
  - check for "impaired" status






