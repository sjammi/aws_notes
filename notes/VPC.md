# Networking

## VPC (Virtual Private Cloud)
- Multiple VPCs per region
- Private, so only private IPs
- Subnets - tied to AZ

Connection pattern:  
VPC can have:  
-> Internet gateway  
-> Router (route tables, for each thing between everything)  
-> VPC Endpoint to (AWS service(s))
-> subnet  
    -> Security group  
    -> EC2 instances  
        NAT Instance, NAT Gateway, Bastion, etc  

-> public subnet  
    -> Bastion host (EC2 instance) to connect to private subnet instance  
    -> NATG  
    -> NAT to connect to internet (outdated, use NATG)  
        -> routes traffic to NAT to and from wherever  
        -> has to be defined in route table  
        -> Add an Elastic IP to route with  
-> private subnet  
    -> Must allow traffic in SG from Bastion host  


---

## Subnet
- 5 IPs reserved by default**

## IGW (Internet Gateway)
- allow resources in VPC to connect to internet
  - WITH Route Table modification
- Add IGW to VPC, then modify Route Table to point IPs to the IGW for internet traffic

---

## NACL (Network Access Control Lists)
- Handles reqs to subnet
  - vs SG inside subnet
- Ranked by rule number, lower takes precedence

---

## VPC Endpoints
- Connect stuff in my VPC to other AWS services
- TIED TO SPECIFIC REGION
- Interface vs Gateway endpoints
  - Interface:
    - provision ENI (private IP) attached to SG
    - Per hour, per GB
  - Gateway: provision gateway to connect to via route table
    - S3 + Dynamo
    - Free
- ## For exam: gateway in general, interface for connection to on-premises

---

## Flow logs
- At VPC, Subnet, or ENI level 
- NACL or SG issue?
  - Incoming:
    - in REJECT -> either
    - in ACCEPT, out REJECT -> NACL
  - Outgoing:
    - out REJECT -> either
    - out ACCEPT, in REJECT -> NACL

---

## Site to Site VPN
- VPG (Virtual Private Gateway)
  - VPN concentrator on AWS side
  - attached to VPN where you want site-to-site conn
- CGW (Customer Gateway)
  - using client side public IP OR NAT device with public IP
    - ## requires route propogation on VPG
- Cloudhub
  - hub and spoke model
  - VGW -> many CGWs
  - Allows connection between CGWs as well
  - connect VPNs to VGW, configure dynamic routing and route tables

---

## Transit Gateway
- peering between thousands of VPCs
- hub and spoke
- share across accounts with RAM
- limit via Route Tables
- supports IP Multicast
- ECMP - Equal Cost Multi Path
  - Multiple site-to-site VPN connections, increased bandwidth
- works across accounts

---

## IPv6
- all public and internet routable
- Dual stack mode: private v4 and public v6 at min

---

## PrivateLink / VPC Endpoint Services
- connect client <-> host VPCs privately
- doesn't need any routing or anything
- Only usable with NLB and ENI

---

## Cost (per GB)
- free traffic into EC2
- free between same AZ instances on private IP
- costs a little for elastic or public IP between AZs
  - costs half with a private IP
- inter-region more expensive
- Keep traffic in AWS to minimize costs
- 

