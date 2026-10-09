---
type: infrastructure
certs: [CLF, SAA, DVA, SOA]
---
# AWS Infrastructure

There are two types:
- [[Region]]s: continents or countries, geographically spread.
- EDge locations: smaller than regions, have less services than regions.

Regions benefits:
1. Geographically separation --> Isolate Fault domain.
2. Geopolitical separation --> different governance.
3. Location control --> performance tuning on latency.

Inside each regions, there are multiple [[Availability Zone]]s (AZ). Not only a data center. [[Virtual Private Cloud]] (VPC) is across multiple AZ

THere are three levels of resillient:
- Globally
- [[Region]]s
- [[Availability Zone]]