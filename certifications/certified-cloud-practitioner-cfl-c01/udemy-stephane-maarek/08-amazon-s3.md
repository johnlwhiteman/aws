# 08: Amazon S3

## Overview

* Infinite scaling storage
* AWS services use it

### Use Cases

* Backup and storage
* Disaster recovery
* Archive
* Hybrid cloud storage
* Application hosting
* Media hosting
* Data lakes & big data anlytics
* Software delivery
* Static websites
* Nasdaq stores 7 years of data into S3 Glacier

### S3 Buckets

* Stores objects (files) in "buckets" (directories)
* Buckets must have a globaly unique name (across all regions all accounts)
* Buckets are defined at the region level
* S3 looks like a global service but buckets are created in a region
* Naming convention
  * No uppercase, no underscore
  * 3-63 characters long
  * Not an IP
  * Must start with lowercase letter or number
  * Must NOT start with the prefix xn--
  * Must NOT end with the suffix --s3alias

### S3 Objects

* Objects (files) have a key
  * Keys are very long names that contain slashes ("/")
* The *key* is the FULL path:
  * s3://my-bucket/*my_file.txt*
  * s3://my-bucket/*my_folderI/another_foler/my_file.txt*
* The key is composed of prefix + object name
  * s3://my-bucket/*my_folder/another_folder/my_file.txt*
* There's not concept of "directories" within buckets
  * (although the UI will trick you to think otherwise)
* Object values are the content of the body
  * Max object size is 5TB (5000GB), must use "multi-part upload"
* Metadata (list of  text key / value pairs - system or user metadata)
* Tags (Unicode key / value pair - up to 10) -- useful for security / lifecycle
* Version ID (if versioning is enabled)

## S3 Security: Bucket Policy

* User-based
  * IAM Policies - which API calls should be allowed for a specific user from IAM
* Resource-based
  * Bucket Policies - bucket wide rules from the S3 console - allows cross account
  * Object Access Control List (ACL) - finer grained (can be disabled)
  * Bucket Access Control List (ACL) - less common (can be disabled)
* Note: An IAM principal can access an S3 object if:
  * The user IAM permissions ALLOW it OR the resource policy ALLOWS it
  * AND there's not explicit DENY
* Encryption: encrypt objects in Amazon S3 using encryption keys


### S3 Bucket Policies

* JSON based policies
  * Resources: buckets and objects
  * Effect: Allow / Deny
  * Actions: Set of APIs to Allow or Deny
  * Principal: The account or user to apply the policy to
* Use S3 bucket for policy to:
  * Grant public access to the bucket
  * Force objects to be encrypted at upload
  * Grant access to another account (Cross Account)
* Bucket setting for block public access
  * These settings were created to prevent company data leaks
  * If you know your bucket should never be public, leave these on
  * Can be set at the account level

## S3 Security Website Overview

* S3 can host static websites and have them accessible on the Internet
* The website URL will be (depending on the region)
  * http://bucket-name.s3-website-aws-region.amazonaws.com
  * http://bucket-name.s3-website.aws-region.amazonaws.com

## S3 Versioning Overview

* You can version your files in Amazon S3
* It is enabled at the bucket level
* Same key overwrite will change the "version": 1,2,3...
* It is best practice to version your buckets
  * Protect against unintended deletes (ability to restore version)
  * Easy roll back to a previous version
* Notes:
  * Any file that is not versioned prior to enabling versioning will have version "null"
  * Suspending versioning does not delete the previous version


## S3 Replication Overview (CRR & SRR)

* Say we want to replicate data in buckets from across regions
* Must enable versioning in the source and destination buckets
* Cross-Region Replication (CRR)
* Same-Region Replication (SRR)
* Buckets can be in different AWS accounts
* Copying is asynchronous
* Must give proper IAM permissions to S3
* Use cases:
  * CRR - compliance, lower latency access, replication across accounts
  * SRR - log aggregation, live replication between production and test accounts

## S3 Storage Classes Overview



## S3 Encryption

## Shared Responsibility Modeling for S3


## AWS Snow Family Overview


## References
