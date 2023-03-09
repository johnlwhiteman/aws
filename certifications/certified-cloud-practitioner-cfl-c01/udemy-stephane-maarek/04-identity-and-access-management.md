# Identity and Access Management (IAM)

## Introduction: Users, Groups, Policies

* Global service
* Root account created by default, shouldn't be used or shared
* Users are people in your org and be added to groups
* Groups only contain users, not other groups
* Users don't have to belong to a group, and a user can belong to multiple groups
* Users and groups can be assigned JSON documents called policies
  * These policies define the permissions of the users
  * In AWS, you apply the least privilege principle: don't give more permissions than a user needs

## IAM Users & Groups Hands On

* See demo

## IAM Policies


### Group Policies

* We can attach a policy at the group level and all users in the group will inherit that policy

### Inline Policies

* Attached only to a user 

### Policy Structure

* JSON
* Version
* ID
* Statement(s)
  * SID - statement ID (optional)
  * Effect - allows or denies something
  * Principal - account/user/role to which the policy applies to
  * Action - list of actions this policy allows or denies
  * Resource - list of resources to which the actions applied to
  * Condition - conditions for when this policy is in effect (optional)

## IAM - MFA Overview

### Password Policy

* Strong passwords = higher security for your account
* In AWS, you can setup a password policy
  * Set a minimum password length
  * Require specific character types
    * Uppercase, lowercase letters
    * Numbers
    * Non-alphanumeric characters
* Allow users to change their own passwords
* Require users to change their passwords after some time (expiration)

### Multi-factor Authentication (MFA)

* Users have access to your account and can possibly change configurations or delete resources in your AWS account
* You want to protect your Root Accounts and IAM users
* MFA = password you know + security device you own
* Virtual MFA Device
  * Google Authenticator (phone only), Authy (multi-device)
  * Supports multiple tokens on a single device
* Universal 2nd Factor (U2F) Security Key
  * Physical device 
  * YubiKey by Yubico (3rd party)
  * Supports multiple users/roots
* Hardware Key Fob MFA device
  * Gemalto (3rd party)
* Hardware Key Fob MFA Device for AWS GovCloud (US)
  * SurePassId (3rd party)

## AWS Access Keys, CLI, and SDK

### Three options to access AWS

1. AWS Management Console (protected by password + MFA)
2. AWS Command Line Interface (CLI): protected by access keys
3. AWS Software Developer Kit (SDK) - for code: protected by access keys

* Access keys are generated through the AWS console
* Users manage their own access keys
* Access keys are secret, just lik a password. Don't share them
* `Access Key ID ~= username`
* `Secret Access Key ~= password`

### What's the AWS CLI?

* A tool that enables you to interact with AWS services using commands in your command-line shell
* Direct access to the public APIs of AWS services
* You can develop scripts to manage your resources
* It's open-source: `https://github.com/aws/aws-cli`

### What's the AWS SDK?

* AWS Software Development Kis (AWS SDK)
* Language-specific APIs (set of binaries)
* Enables you to access and manage AWS services programmatically
* Embedded within your application
* Supports 
  * SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
  * Mobile SDKs (Android, iOS, ...)
  * IoT Device SDKs (Embedded C, Arduino, ...)
* AWS CLI is built on the AWS SDK for Python (boto)

## AWS CloudShell

* Alternative to CLI on local machine
* Not available everywhere
* A terminal in the cloud

## IAM Roles for AWS Services

* Some AWS services will need to perform actions on your behalf
* To do so, we will assign permissions to AWS services with IAM roles
* Common roles
  * EC2 Instance Roles
  * Lambda Function Roles
  * Roles for CloudFormation

## IAM Security Tools

* IAM Credentials Report (account-level)
  * A report that lists all your account's users and the status of their various credentials
* IAM Access Advisor (user-level)
  * Access advisor shows the service permissions granted to  a user and when those service were last accessed
  * You can use this information to revise your policies to align with the principle of least privilege

## IAM Guidelines and Best Practices

* Don't use the root account except for AWS account setup
* One physical user = One AWS user
* Assign users to groups and assign permissions to groups
* Create a strong password policy
* Use and enforce the use of Multi Factor Authentication (MFA)
* Create and use roles for giving permissions to AWS services
* Use access keys for programmatic access (CLI/SDK)
* Audit permissions of your account with the IAM Credentials Report
* Never share IAM users & access keys

## Shared Responsibility Model for IAM

* For AWS
  * Infrastructure (global network security)
  * Configuration and vulnerability analysis
  * Compliance validation

* For You
  * Creating groups, roles, policies, management, and monitoring
  * Enable MFA on all accounts
  * Rotate all your keys often
  * Use IAM tools to apply appropriate permissions
  * Analyze access patterns and review permissions

## Summary

* Users: Mapped to a physical user, has a password for AWS console
* Groups: Contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: For EC2 instances or AWS services
* Security: Multi factor authentication + password policy
* CLI: Manage your AWS services via the command line
* SDK: Manage your AWS services via a programming language
* Access Keys: Access using CLI or SDK
* Audit: IAM Credential Reports and IAM Access Advisor


## Quiz

* What is a proper definition of IAM Roles?

`An IAM entity that defines a set of permissions for making AWS service requests, that will be used by AWS services`

What are IAM Policies?

`JSON documents to define Users, Groups, or Roles' permissions`


## References

