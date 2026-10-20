---
type: service
section: fundamentals
certs: [CLF, SAA, DVA, SOA]
tags: [infrastructure, authentication, authorization, fundamentals, global]
---
# Identity and Access Management (IAM)

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

## Access keys

Long-term credentials on AWS.

Differences to Username & Password:
1. IAM User has 1 username, and 1 password. An IAM user can have **two access keys**, no more.
2. Access keys can be created, updated, deactivate or activate.

## [[Policies]]

Policies are attached to [[identities]] inside AWS.

Grant [[access]] or deny [[access]] by one or more [[statement]]s in IAM policy documents, which are in JSON Format.

A [[statement]] contains:
- `Sid`: statement ID
- `Effect`: [[Allow]] or [[Deny]]
- `Action`: a list of actions, whose formats are `<server>:<action>`, or _wildcard_ formats.
- `Resource`: a list of resources, URI or wildcard.

The order or the priority:
1. Explicit [[Deny]]
2. Explicit [[Allow]]
3. Default (implicit) [[Deny]]

There are two types of policies:
- **Inline Policies**: apply [[JSON]] documents for each accounts. We should use this for exceptional Allow or Deny.
- **Managed Policies**:
  - Can be reusable.
  - Help to low management overhead.
- There are two sub-types:
  - AWS Manage policies.
  - Customized policies.

## IAM Users

IAM Users are an identity used for anything requiring **long-term** AWS access, e.g _Humans_, _Applications_, or _Service accounts_

A **Principal** can be a user or an application.

[[Authentication]] is a process to proove a _principal_ is what it claims to be.

[[Authorization]] is checking the [[statement]]s.

## Other notes

### Limit of account and group

An AWS account can has only **5,000 IAM users** in maximum.

An IAM User can be member of **max 10 groups**.

If you meet that limitations, you can fix by using IAM [[Roles]] & [[Identity Federation]].

## Read more

- [[Amazon Resource Name]] or [[ARN]]