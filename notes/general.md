## Global Infra:
- regions
  - "us-east-1"
  - cluster of data centers
  - compliance (data governance, legal reqs), proximity, available services, pricing
- availability zones
  - 3-6 per region
    - "us-east-1a", "us-east-1c" ...
    - one or more isolated data centers
- data centers
- edge locations / points of presence

---

## Terms:
As a Service  
- IaaS - Infra  
- Saas - Software  
- Paas - Platform  

Load balancing
- servers that forward traffic to more servers
- good for single access point (DNS)
- Provides SSL termination (HTTPS)
- Separate public and private traffic

---

## Scalability VS Availability:
- Vertical and horizontal scalability
- High Availability:
  - ## goal to survive data loss
  - app/system runs in at least 2 AZ
  - passive (RDS in multiple AZ)
  - active (horizontal scaling)
- Horizontal scaling
  - ## ASG or LB

