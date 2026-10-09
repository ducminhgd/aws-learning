---
type: service
certs: [CLF, SAA, DVA, SOA]
---
# Amazon Machine Image (AMI)

An [[Amazon Machine Image]] can be used to create [[EC2]] instances or can be created from an [[EC2]] instance.

AMI contains:
- Attached permissions
  - Public - Everyone allowed
  - Owner - Implicit allow
  - Explicit: specific AWS accounts allowed
- Boot volume: the boot volume for the OS - root volume for Linux or C drive for Windows.
- Block Device Mapping: a configuration of volumes of AMI has map to the volume of the instances.