VPC and VPN shit
NAT
Security group details
SQS details

Internet gateway: VPC component to allow internet comm

Bastion host: sit in public subnet to handle SSH or RDP conn with private subnets

Egress-only: VPC component for outbound comm over IPv6


## NAT (Network Access Translation):
- EC2 instances on private subnets -> internet
- Must be in public subnet
- must have elastic IP
- route tables to route private subnets to NAT
- NAT gateway
  - AWS managed
  - pay per hour and bandwidth
  - can't be used by EC2 in same subnet
  - No security groups needed
- Instance vs Gateway
  - gateway highly available in AZ
  - Instance depends on EC2 instance
    - cost, speed
  - Instance can be bastion host

---

## CIDR (Classless Inter Domain Routing)
- Allocate IP addresses
- ##.##.##.##/##
  - Base IP
  - subnet mask
    - represents how much of base IP is variable

---



