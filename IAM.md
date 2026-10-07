---
type: service
certs: [CLF, SAA, DVA, SOA]
---
# IAM - Identity and Access Management

It contains 3 types of objects: **Users**, **Groups**, and **Roles**.

- **Users** represent *humans* or *applications*.
- **Groups** represent *collections* of related *users*.
- **Roles** can be used by AWS Services or you want to grant external access. They are often used when the numbers of identities are uncertain.

IAM is a globally resilient service, an IAM in a specific AWS Account is your own dedicated instance of IAM separate from other accounts and from anyone else's accounts. Your AWS account trusts your instance of IAM.

IAM also defines the policies to allow or to deny access to AWS services. Policy takes effects when it is attached into the identities.

IAM has three main jobs:

- Manages Identites or ID Provider (IDP).
- Authenticate.
- Authorize.

IAM is provided free, no cost.

IAM only controls local identities of your account.