## Overall:
- root account made by default, create more users
- organizations and groups
    - no groups in groups, users in one/many/no groups

---

## Permissions:
- Policies (json)
- LEAST PRIVILEDGE PRINCIPLE

---

## Structure:
```
{
  "Version": language version. Currently always "2012-10-17”
  "Id": anything, *optional
  "Statement": [{
    "Sid": anything, *optional
    "Effect": (Allow, Deny)
    "Principal": account/user/role to which this policy applied to
    "Action": (list of actions this policy allows or denies) [
      "s3:getObject"
      ]
    "Resource": (list of resources to which the actions applied to) [
      "arn:aws:..."
      ]
    "Condition": conditions for when this policy is in effect *optional
  }]
}
```

---

## Password Policy:
- set min length
- require all chars (uppercase, lowercase, numbers, non-alphanumeric), 
- enforce expiration limit
- allow change own pw's
- prevent pw reuse

---

## Security Tools:
- Credentials Report (account level): users statuses and their creds
- Access Advisor (user level): permissions granted, last used, modify policies


---

## Best Practices:
- one physical user = one AWS user = IRL person
- users -> groups, group -> permissions
- Strong pw's and MFA
- Roles for permissions to services


