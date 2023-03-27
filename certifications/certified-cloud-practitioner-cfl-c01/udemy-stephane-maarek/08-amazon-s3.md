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

* Amazon S3 Standard- General Purpose
* Amazon S3 Standard - Infrequent Access (IA)
* Amazon S3 One Zone - Infrequent Access
* Amazon S3 Glacier Instant Retrieval
* Amazon S3 Glacier Flexible Retrieval
* Amazon S3 Glacier Deep Archive
* Amazon S3 Intelligent Tiering
* Can move between classes manually or using S3 Lifecycle configurations

## S3 Durability and Availability

* Durability:
  * High durability (99.999999999%, 11 9's) of objects across multiple AZ
  * If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
  * Same for all storage classes

* Availability:
  * Measure how readily available a service is
  * Varies depending on storage class
  * Example: S3 standard has 99.99% availability = not available 53 minutes a year

## S3 Standard - General Purpose

* 99.99% Availability
* Used for frequently access data
* Low latency and high throughput
* Sustain 2 concurrent facility failures
* Use Cases: Big data analytics, mobile & gaming applications, content distribution

## S3 Storage Classes - Infrequent Access

* For data that is less frequently accessed, but requires rapid access when needed
* Lower cost than S3 Standard

### S3 Standard - Infrequent Access (S3 Standard-IA)

* 99.9% availability
* Use cases: disaster recovery, backups

### S3 One Zone - Infrequent Access (S3 One Zone-IA)

* High durability (99.999999999%) in a single AZ
* Data lost if AZ is destroyed
* 99.5% availability
* Use cases: Storing secondary backup copies of on-premise data, or data that you can recreate

## S3 Glacier Storage Classes

* Low-cost object storage meant for archiving / backup
* Pricing - pricing for storage + object retrieval cost

* Amazon S3 Glacier Instant Retrieval
  * Millisecond retrieval, great for data accessed once a quarter
  * Minimum storage duration is 90 days
* Amazon S3 Glacier Flexible Retrieval (formerly Amazon S3 Glacier)
  * Expedited (1 to 5 minutes), Standard (3 to 5 hours), Bluk (5 to 12 hours) - free
  * Minimum storage duration of 90 days
* Amazon S3 Glacier Deep Archive - for long term storage
  * Standard (12 hours), Bulk (48 hours)
  * Minimum storage duration of 180 days

## S3 Intelligent-Tiering

* Small montly monitoring and auto-tiering fee
* Moves objects automatically between Access Tiers based on usage
* There are no retrieval charges in S3 Intelligent-Tiering
* Frequent Access tier (automatic): default tier
* Infrequent Access tier (automatic): objects not accessed for 30 days
* Archive Instant Access tier (automatic): objects not accessed for 90 days
* Archive Access tier (optional): configurable from 90 days to 700+ days
* Deep Archive Access tier (optional): config. from 180 days to 700+ days

## S3 Encryption

* Server side encryption is available and used by default
* Client side encryption - user encrypts file before uploading
* Both models are available with server side encryption always on

## Shared Responsibility Modeling for S3

* AWS
  * Infrastructure (global security, durability, availability, sustain concurrent loss of data in two facilities)
  * Configuration and vulnerability analysis
  * Compliance validation

* YOU
  * S3 versioning
  * S3 bucket policies
  * S3 replication setup
  * Logging and monitoring
  * S3 storage class
  * Data encryption at rest and in transit

## AWS Snow Family Overview

* Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS
  * Data migration
    * Snowcone
    * Snowball Edge
    * Snowmobile
  * Edge computing
    * Snowcone
    * Snowball Edge
* Anything snowball gets an AWS device, usually shipping and not over a network

### Snowball Edge (for data transfers)

* Physical data transport solution: move TBs or PBs of data in or out of AWS
* Alternative to moving data over the network (and paying network fees)
* Pay per data transfer job
* Provide block storage and Amazon S3-compatible object storage
* Snowball Edge Storage Optimized
  * 80 TB of HDD capacity for block volume and S3 compatible object storage
* Snowball Edge Compute Optimized
  * 42 TB of HDD capacity for block volume and S3 compatible object storage
* Use cases: large data cloud migrations, DC decommission, disaster recovery

### Snowcone & Snowcone SSD

* Small, portable computing, anywhere, rugged & secure, withstands harsh environments
* Light (4.5 pounds, 2.1 kg)
* Device used for edge computing, storage, and data tranfer
* Snowcone - 8TB of HDD Storage
* Snowcone SSD - 14 TB of SSD Storage
* Use Snowcode where Snowball does not fit (space-constrained environment)
* Most provide your own battery / cables
* Can be sent back to AWS offline, or connect to a Internet and use `AWS DataSync` to send data


### AWS Snowmobile

* An actual truck
* Transfer exabytes of data (1 EB = 1,000 PB = 1,000,000 TBs)
* Each Snowmibile has 100 PB of capacity (use multiple in parallel)
* High security: temperature controlled, GPS, 24/7 video surveillance
* Better than Snowball if you transfer more than 10 PB


### Snow Family - Usage Process

* Request Snowball devices from the AWS console for delivery
* Install the snowball client / AWS OpsHub on your servers
* Connect the snowball to your servers and copy files using the client
* Shop back the device when you're done (goes to the right AWS facility)
* Data will be loaded into an S3 bucket
* Snowball is completely wiped

### What is Edge Computing?

* Process data while it's being created on an edge location
  * An edge location is something not on the network/cloud
    * A truck on the road, a ship on the sea, a mining station underground ...
    * These locations may have limited / no Internet access
    * Limited / no easy access to computing power
* We setup a Snowball Edge / Snowcone device to do edge computing
* Use cases for Edge Computing
  * Preprocess data
  * Machine learning at the edge
  * Transcoding media streams
* Eventually (if need be) we can ship back the device to AWS (for transferring data for example)
* Snowcone & Snowcone SSD (smaller)
  * 2 CPUs, 4 GB of memory, wired or wireless access
* Snowball Edge - Compute Optimized
    * 104 vCPUs, 416 GiB of RAM
    * Optional GPU (useful for video processing or machine learning)
    28 TB NVMe or 42TB HDD usable storage
* Snowball Edge - Storage Optimized
  * Up to 40 vCPUs, 80 GiB of RAM
  * Object storage clustering available
* All: Can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)
* Long-term deployment options: 1 and 3 years discounted pricing

### AWS OpsHub

* Historically, to use Snow Family devices, you needed a CLI (Command line interface tool)
* Today, you can use AWS OpsHub (a software you install on your computer / laptop) to manage your Snow Family Device
* Graphical interface (GUI)
  * Unlocking and configuring single or clustered devices
  * Transferring files
  * Launching and managing instances running on Snow Fmaily Devices
  * Monitor device metrics (storage capacity, active instances on your device)
  * Launch compatible AWS services on the devices (ex:Amazon EC2 instances, AWS DataSync, Network File System (NFS))

## Storage Gateway Overview

### Hybrid Cloud for Storage
* AWS is pushing for "hybrid cloud"
  * AWS is pushing for "hybrid cloud"
    * Part of your infrastructure is on the cloud
    * Part of your infrastructure is on on-premises
* This can be due to:
  * Long cloud migrations
  * Security requirements
  * Compliance requirements
  * IT strategy
* S3 is a proprietary storage technology (unlike EFS/NFS), so how do you expose the S3 data on-premise?
* AWS Storage Gateway

* Block
  * Amazon EBS
  * EC2 Instance Store
* File
  * Amazon EFS
* Object
  * Amazon S3
  * Glacier

### AWS Storage Gateway

* Bridge between on-premise data and cloud data in S3
* Hybrid storage service to allow on-premises to seamlessly use the AWS cloud
* Use cases: disaster recovery, backup, and restore, tiered storage
* Types of Storage Gateway:
  * File Gateway
  * Volume Gateway
  * Tape Gateway
* No need to know the types at the exam

## Summary

* Buckets and Objects: global unique name, tied to a region
* S3 security: IAM policy, S3 Bucket Policy (public access), S3 Encryption
* S3 Websites: host a static website on Amazon S3
* S3 Versioning: multiple version for files, prevents accidental deletes
* S3 Replication: same-region or cross-region, must enable versioning
* S3 Storage Classes: standard, IA, IZ-IA, Intelligent, Glacier (Instant, Flexible, Deep)
* Snow Family: import data onto S3 through a physical device, edge computing
* OpsHub: desktop application to manage Snow Family devices
* Storage Gateway: hybrid solution to extend on-premise storage to S3

## Quiz

* Which S3 Storage Class is the most cost-effective for archiving data with no retrieval time requirement? - Amazon Glacier

* What hybrid AWS service is used to allow on-premises servers to seamlessly use the AWS Cloud at the storage layer? - Storage Gateway

* Which of the following services is a petabyte-scale data moving service (as a fleet) in or out of AWS with computing capabilities? - Snowball Edge. Snowball Edge is best-suited to move petabytes of data and offers computing capabilities. Be careful, it's recommended to use a fleet of Snowballs to move less than 10PBs of data. Over this quantity, it's better-suited to use Snowmobile.

* Which of the following is an exabytes-scale data moving service in or out of AWS? - Snowmobile - Snowmobile is used to move exabytes of data in or out of AWS (1 EB=1,000 PBs=1,000,000 TBs).

* A research team deployed in a location with low-internet connection would like to move 5 TBs of data to the Cloud. Which service can it use? - Snowcone - AWS Snowcone is a small, portable, rugged, and secure edge computing and data transfer device. It provides up to 8 TB of usable storage.

* What can you use to define actions to move S3 objects between different storage classes?

* What can you use to define actions to move S3 objects between different storage classes? Lifecycle Rules can be used to define when S3 objects should be transitioned to another storage class or when objects should be deleted after some time.

* A non-profit organization needs to regularly transfer petabytes of data to the cloud and to have access to local computing capacity. Which service can help with this task? Snowball Edge Storage Optimized devices are well suited for large-scale data migrations and recurring transfer workflows, as well as local computing with higher capacity needs.

* Which S3 Storage Class is suitable for less frequently accessed data, but with rapid access when needed, while keeping a high durability and allowing an Availability Zone failure? - Amazon S3 Standard-Infrequent Access allow you to store infrequently accessed data, with rapid access when needed, has a high durability, and is stored in several Availability Zones to avoid data loss in case of a disaster. It can be used to store data for disaster recovery, backups, etc.

## References
