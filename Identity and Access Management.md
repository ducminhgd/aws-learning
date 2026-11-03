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

## IAM groups

[[IAM Groups]] are containers for Users, `n:n` relationship.

### IAM Group Limitations

While IAM groups help with user management, there are important limitations:

#### 1. No Nested Groups

You cannot nest IAM groups. A group can only contain users, not other groups.

#### 2. Group Limits
  
- There is a limit of **300 groups** per [[AWS account]], but this can be increased with a support request.
- Users can belong to up to **[[10 groups]]**, and there is a hard limit of **[[5,000 IAM users]] per account**.

#### 3. No "All Users" Group

Unlike some identity management systems, IAM does not provide a built-in "All Users" group. If needed, you would have to manually create a group and add all users to it.

### Benefits of Using IAM Groups

IAM groups offer two primary benefits:

#### 1. Effective User Management

- Groups help organize users by teams, roles, or other criteria. You can create groups to represent departments or projects and assign users accordingly. This simplifies the management of permissions.

#### 2. Policy Attachment

- **Policies** (both **in-line** and **managed**) can be attached to IAM groups.
- When a user is added to a group, they inherit all the permissions associated with that group.
- For example, if _Sally_ is a member of the **Developers Group** (which has a policy attached) and also the **QA Group** (with another policy), she inherits permissions from both groups. In addition, she may have **directly attached policies** as well.

#### Policy Combination Example:

- _Sally_ has three sources of permissions:
  - **Developers Group Policy**
  - **QA Group Policy**
  - **Sally’s Direct Policy**

AWS evaluates all these policies together to determine what actions _Sally_ is allowed or denied.

## IAM roles

An [[IAM role]] is one type of identity that exists within an [[AWS account]]. The other identity type, which we’ve already covered, is the [[IAM user]]. Both users and roles fall under the category of "principals," which represent entities (e.g., people, applications, or processes) that authenticate with AWS.

### How IAM Roles Work

IAM roles do not represent a specific person or entity long-term. Instead, a role represents a **set of permissions** that a principal can assume temporarily. When an identity (human, service, or application) assumes a role, they "become" that role and inherit its permissions for a limited time.

#### Assumption of Roles

When an identity assumes an IAM role, they gain access to any permissions the role has. For example, an external mobile app can assume a role in your AWS account and temporarily access resources like an [[S3]] bucket.

#### Temporary Credentials

AWS generates **temporary security credentials** for identities that assume a role. These credentials:

- Expire after a set time.
- Must be renewed by re-assuming the role.

Temporary credentials behave similarly to long-term **access keys**, but are only valid for short periods. Every time these temporary credentials are used, they are checked against the **role’s permissions policy**.

### Policies Associated with IAM Roles

IAM roles have two primary policies attached to them:

1. **Trust Policy**: Controls which identities (users, applications, or services) are allowed to assume the role. This can reference:

    - IAM users or roles in the same AWS account.
    - AWS services like EC2.
    - External identities (e.g., users in other AWS accounts, or federated identities such as Google or Facebook users).

    Example: Identity A is allowed to assume the role, while Identity B is denied based on the trust policy configuration.

2. **Permissions Policy**: Dictates what actions the assumed role can perform on AWS resources. This policy grants permissions to resources like S3, EC2, etc.

### Why Use Roles?

- **Security**: Avoids the security risk of hard-coded access keys.
- **Flexibility**: Handles multiple invocations of the Lambda function efficiently (whether it's 1 or 100).
- **Short-term Permissions**: The temporary credentials expire after the task is complete.

### Service-Linked Roles

A **[[Service-Linked Role]]** is a specialized IAM role directly associated with a specific AWS service. These roles have predefined permissions that allow the service to interact with other AWS services on behalf of the user. The creation, modification, and deletion of these roles are managed by the service itself and may vary depending on the specific service.

The key characteristics of a Service-Linked Role are:

1. **Predefined Permissions**: The service defines the permissions required to perform actions on other AWS services.
2. **Role Management**: The AWS service can automatically create or delete the role, or allow the user to manage the role through IAM or within the service's setup process.
3. **Deletion Restrictions**: You cannot delete a service-linked role unless it is no longer being used by the associated service.

A **Service-Linked Role** can only be deleted once it is no longer in use by its associated service. This ensures that you don't accidentally remove a role that is critical for an AWS service's operation.

### Role Separation

**Role Separation** refers to the practice of separating responsibilities across different job roles. For example, one team might be responsible for creating IAM roles, while another team may only have permission to use the roles.

#### PassRole Permissions

To allow a user (e.g., Bob) to use an existing role without modifying or creating it, you can assign **PassRole** permissions. This allows Bob to pass an existing role into an AWS service, but he won't have permissions to create or modify roles.

An example policy for **PassRole** might look like this:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iam:PassRole",
      "Resource": "arn:aws:iam::account-id:role/service-role-name"
    }
  ]
}
```

With this permission, Bob can configure an AWS service using a role that has already been created by another team.

### Real-World Application of PassRole

One common use case for **PassRole** is with **CloudFormation**. Normally, when you create a CloudFormation stack, it uses the permissions of your IAM identity. However, you can assign a specific role for CloudFormation to use, which may have broader permissions than your own. This allows for greater flexibility in defining which AWS resources the stack can create.

## [[Secure Token Service]] (STS) and IAM Roles

When an identity assumes a role, AWS uses a service called **Secure Token Service (STS)** to generate temporary credentials. The operation involved in assuming a role is known as `sts:AssumeRole`.

## Other notes

### Limit of account and group

An AWS account can has only **[[5,000 IAM users]]** in maximum.

An IAM User can be member of **max [[10 groups]]**.

If you meet that limitations, you can fix by using IAM [[Roles]] & [[Identity Federation]].

## Read more

- [[Amazon Resource Name]] or [[ARN]]