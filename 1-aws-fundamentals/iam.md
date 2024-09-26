# IAM: Identity and Access Management

This is a **Global service**

Root account is created by default.
When accessing AWS, the root account should **never** be used or shared. Users must be created with the proper permissions. IAM is central to AWS.
- Users: A physical person
- Groups: Functions (admin, devops) Teams (engineering, design) which contain a group of users
          Groups can only contain users, not the other groups.
          It's not necessary that a user should belong to a group.(not a best practice) 
          In the same way a user can also belong to multiple groups.
- Roles: Internal usage within AWS resources
- Policies (JSON documents): Defines what each of the above can and cannot do. **Note**: IAM has predefined managed policies.


#### For big enterprises:
- IAM Federation: Integrate their own repository of users with IAM using SAML(Security Assertion Markup Language) standard

### Policies
IAM policies define permissions for an action regardless of the method that you use to perform the operation.

### IAM Policies Structure
IAM Policies consists of 
  -Version: policy language version, (Always include) "2024-09-25"
  -Id: an identifier for the policy (optional)
  -Statement: one or more individual statements (required)
              -Sid: an identifier for the statement(optional)
              -Effect: whether the statement allows or denies access(Allow,Deny)
              -Principal: account/user/role to which this policy applied to
              -Action: list of actions this policy allows or denies
              -Resource: list of resources to which the actions are applied to
    
#### Policy types
- Identity-based policies
  - Attach managed and inline policies to IAM identities (users, groups to which users belong, or roles). Identity-based policies grant permissions to an identity.

- Resource-based policies
  - Attach inline policies to resources. The most common examples of resource-based policies are Amazon S3 bucket policies and IAM role trust policies. Resource-based policies grant permissions to a principal entity that is specified in the policy. Principals can be in the same account as the resource or in other accounts.

- Permissions boundaries
  - Use a managed policy as the permissions boundary for an IAM entity (user or role). That policy defines the maximum permissions that the identity-based policies can grant to an entity, but does not grant permissions. Permissions boundaries do not define the maximum permissions that a resource-based policy can grant to an entity.

- Organizations SCPs
  - Use an AWS Organizations service control policy (SCP) to define the maximum permissions for account members of an organization or organizational unit (OU). SCPs limit permissions that identity-based policies or resource-based policies grant to entities (users or roles) within the account, but do not grant permissions.

- Access control lists (ACLs)
  - Use ACLs to control which principals in other accounts can access the resource to which the ACL is attached. ACLs are similar to resource-based policies, although they are the only policy type that does not use the JSON policy document structure. ACLs are cross-account permissions policies that grant permissions to the specified principal entity. ACLs cannot grant permissions to entities within the same account.

- Session policies
  - Pass advanced session policies when you use the AWS CLI or AWS API to assume a role or a federated user. Session policies limit the permissions that the role or user's identity-based policies grant to the session. Session policies limit permissions for a created session, but do not grant permissions. For more information, see Session Policies.

#### AWS Policy Simulator
- When creating new custom policies you can test it here:
  - https://policysim.aws.amazon.com/home/index.jsp
  - This policy tool can you save you time in case your custom policy statement's permission is denied
- Alternatively, you can use the CLI:
    - Some AWS CLI commands (not all) contain `--dry-run` option to simulate API calls. This can be used to test permissions.
    - If the command is successful, you'll get the message: `Request would have succeeded, but DryRun flag is set`
    - Otherwise, you'll be getting the message: `An error occurred (UnauthorizedOperation) when calling the {policy_name} operation`

#### IAM - Password Policy
-Strong password = higher security for your account
-In aws, you can setup a password policy:
    -Set a minimum password length
    -Require specific character types
        -including uppercase letters
        -lowercase letters
        -numbers
        -non-alphanumeric characters
    -Allow all IAM users to change theeir own passwords
    -Require users to change their password after some time(password expiration)
    -prevent password re-use
    
  ### MFA - Multi Factor Authentication
  -Users have access to your account and can possibly change configurations or delete resources in your aws account
  -*We have to protect our Root Accounta and IAM users*
  - MFA = password you know + security device you own
  - main benifit **if a password is stolen or hacked, the account is not compromised**
    example: -virtual MFA device -- support for multiple token on a single device
                  -google authenticator(phone only)
                  -authy(phone only)
             -universal 2nd factor (U2F) security key -- support for multiple root and IAM users using a single security key
                  -YubiKey by Yubico(3rd party)(physical)
             -Hadware Key Fob MFA Device --provided by Gemalto(3rd party)
             -Hadware Key Fob MFA Device for AWS GovCloud(US) --provided by SurePassID(3rd party)
    
#### Best practices:
- One IAM User per person **ONLY**
- One IAM Role per Application
- IAM credentials should **NEVER** be shared
- Never write IAM credentials in your code. **EVER**
- Never use the ROOT account except for initial setup
- It's best to give users the minimal amount of permissions to perform their job
