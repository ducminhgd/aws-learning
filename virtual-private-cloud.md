---
type: infrastructure
certs: [CLF, SAA, DVA, SOA]
---
# Virtual Private Cloud (VPC)

VPC is a service of private network, is within accross & one region.

Used in hybrid environment: VPC is between Private Network and [[On-premises]]

Used in multi-cloud: VPC between cloud.

By default, VPC is private & isolated.

There are 2 types of VPC:
- *Default VPC*: initially created by AWS, one per region.
- Custom VPC.

The *Default VPC* has one CIDR only and it is always the same `172.31.0.0/16`. *Custom VPCs* have multiple CIDR ranges. And, it can be removed or re-created

A subnet is required to create a resource in your region. You should assign, or AWS will assign for you, a subnet for a specific [[Availability Zone]]. Subnet assigns public IPv4 addresses.

[[Internet Gateway]] (IGW) allows VPC communicate with the Internet and vice versa.