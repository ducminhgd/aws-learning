---
type: infrastructure
section: fundamentals
certs: [CLF, SAA, DVA, SOA]
tags: [infrastructure, dns, network, fundamentals, global]
---
# Route53

Route53 is the [[DNS]] service of AWS, and it has two main services:
- **Register** domains
- Host **Zones** on managed name servers.

It is a **global** service with a single database.

## Register domains

1. Check the top domain with domain registries.
2. Create a zone file
3. Allocate name servers for each domain zone, generally four name servers for a zone.
4. Liasing with the registry with the top level domain.

## Hosted zones

- Zones are defined by **Zone files** in AWS
- A zone file is hosted on four managed name servers.
- A zone can be public or private (liinked to [[Virtual Private Cloud]] or VPC)
- Hosted zone stores records (recordsets)