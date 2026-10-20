---
type: terminology
section: fundamentals
certs: [CLF, SAA, DVA, SOA]
tags: [fundamentals]
---
# Amazon Resource Name or ARN

Uniquely identify resources within any AWS accounts, the format may be:

```
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id
```

If any of those parts no need to mention, we can exclude or omit it, for example `arn:aws:s3:::bucket-name`, we excluded `region` and `account-id` because [[s3]] is a public and global service.