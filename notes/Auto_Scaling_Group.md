## ASG (Auto Scaling Group)
- f r e e
- ... its a group. That automatically scales.
- Ensures min/max
- Registers new instances to LB
- Spins up new instances if one fails

---

## Launch Template
- AMI + Instance Type
- EC2 User Data (bootstrap script)
- EBS volumes
- Security Groups
- SSH keys
- IAM roles
- Network + Subnet setup
- LB info
- min/max size, initial capacity
- Can scale via CloudWatch metric alarms
  - CPU, request count, network in/out, etc

---

## Scaling policy
- Target Tracking
  - simplest
  - "avg CPU 40%"
- Simple / Step
  - If triggered, increase/decrease by X
- Scheduled
- Predictive

---

## Scaling Cooldowns
- Default 300s
- No other ASG activity during cooldown

