## DNS
- Domain Name System
  - hierarchical naming structure
- Components: eg http://api.www.example.com
  - Registrar: route 53, godaddy, etc
  - DNS Records: A, AAAA, CNAME, NS
  - Zone File: Contains DNS records
  - Name Server: Resolves DNS queries
  - TLD (Top Level Domain): .com
  - SLD(Second LD): example.com

---

## DNS Record Types
- A: hostname -> IPv4
- AAAA: hostname -> IPv6
- CNAME: hostname -> another hostname
- NS: Name Servers in Hosted Zone (controls traffic routing)

---

## Route 53
- **Authoritative** DNS (customer can update DNS records)
- Records
  - Domain/subdomain name: example.com
  - Record Type
    - ## Supports: A / AAAA / CNAME / NS
  - Value - (IP)
  - Routing policy
  - TTL - time record is cached
- Hosted Zones
  - Container with records defining how to route traffic
    - Public HZ: route usual internet traffic
    - Private HZ: Routing for internal VPCs
  - $0.50 per month per HZ
- TTL (Time To Live)
  - ## Mandatory for DNS record
  - High (~24hour)
    - less traffic, more outdated records
  - Low (~60sec)
    - More traffic, less outdated, easy to change
    - more $$$$
- CNAME vs Alias
  - CNAME
    - # Only for non root domain
  - Alias
    - hostname -> AWS resource
    - ## Root OR non root domains
    - free

---

## Alias Records
- Extension to DNS functions
- Can be used for top node of DNS name
- Always A/AAAA
- Cannot set TTL
- Targets
  - ## CANNOT set to an EC2 DNS instance
  - ELB, Cloudfront, Gateway, Beanstalk, S3 sites, VPC endpoints, Global Accellerator, R53 Record (in same zone)

---

## Routing Policies
- Not actually routing anything, only request and response
- Policies:
  - Simple
    - ### If multiple options are returned, one is randomly picked
    - no health checks
  - Multi-Value Answer
    - For trafficking to multiple resources
  - Weighted
    - Control % of requests per resource
    - LB between regions, testing app versions, etc
    - ### Set weight to 0 to stop sending
  - Latency based
    - Redirect to close with low latency location
    - ### based on traffic between users and regions
  - Geolocation
    - Solely based on location, not latency
    - requires a default
  - Geoproximity (using Route 53 Traffic Flow feature)
    - route based on resources and location
  - Failover

- ## cannot access private endpoints without CloudWatch
  - monitor endpoint
    - 15 global checkers, > 18% successful reports = healthy
    - Can set to check based on first 5120 bytes of res
  - Calculated) 
    - monitor other health checks
    - OR, AND, NOT
    - up to 256
  - monitor cloudwatch alarms

---

## Domain Registar vs DNS Service
- Buy or register domain with registrar (pay annually)
- Registrar provides DNS usually, but another can be used
- To use external:
  - Update Name Server records on 3rd party site to use R53 NS's





