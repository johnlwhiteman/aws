# 05: EC2 - Elastic Compute Cloud

## AWS Budget Setup

* AWS Billing Dashboard shows monthly costs and forecasts

### AWS Budgets

* Set custom budgets that alert you when you exceed your budgeted thresholds
* Has templates to help setup budget, including zero-spend budget
* Can also assign monthly total budget what you want to spend, no more

## EC2 Basics

* Most popular AWS offering
* EC2 = Elastic Compute Cloud = Infrastructure as a Service
* It mainly consists in the capability of:
  * Renting virtual machines (EC2)
  * Store data on virtual drives (EBS)
  * Distribute load across machines (ELB)
  * Scale the services using an auto-scaling group (ASG)
* Knowing EC2 is fundamental to understand how the cloud works

### EC2 Sizing and Configuration Options

* Linux, Windows. MacOS
* CPU power/cores (CPU)
* RAM
* Storage
  * Network-attached: EBS & EFS
  * Hardware-attached: EC2 Instance Store
* Network card, speed, public IP address
* Firewall rules - security group
* Bootstrap script (configure at first launch): EC2 User Data

### EC2 User Data

* Possible to bootstrap our instances using an EC2 User data script
* Bootstrapping means launching commands when a machine starts
* Script is only run once at the instance first start
* EC2 user data is used to automate boot tasks such as:
  * Installing updates, software, download common files from the Internet, anything
* The EC2 Data Script runs as the root user

### EC2 Instance Types Basics

* t2, c, r, m, ...
  * vCPU, Mem(GiB), Storage, Network Performance, EBS Bandwidth (Mbps)
  * General purpose, compute optimized, memory optimized, storage optimized
* m5.2xlarge
  * m: instance class
  * 5: generation (AWS improves over time)
  * 2xlarge: size within the instance class

## Security Groups and CLassic Ports Overview

### Introduction to Security Groups

* Fundamental to network security in AWS
* Control how traffic is allowed into or out of our EC2 instances
* Security groups only contain allow groups
  * inbound and outbound traffic
* Rules can be referenced by IP or by security group
* Act as a firewall on EC2 instances
* They regulate:
  * Access to ports
  * Authorized IP ranges - IPv4 and IPv6
  * Control of inbound/outbound network
    * Type, Protocol, Port Range, Source, Description
* Can be attached to multiple instances
* Locked down to a region / VPC combination
* Live "outside" the EC2 - if traffic is blocked and EC2 instance won't see it
* It's good to maintain one separate security group for SSH access
* If your application is not accessible (time out) then it's a security group issue
* If your application gives a "connection refused" error, then it's an application error or it's not launched
* All inbound traffic is blocked by default
* All outbound traffic is authorized by default

### Referencing Other Security Groups

* You can add to the rules the reference to another security group

### Classic Ports to Know

* 21: FTP (File Transfer Protocol)
* 22: SSH (Secure Shell) Linux
* 22: SFTP (Secure File Transfer Protocol)
* 80: HTTP (Unsecure Websites)
* 442: HTTPS (Secure Websites)
* 3389: RDP (Remote Desktop Protocol) Windows

## SSH Overview and Troubleshooting

* Linux / Max / Windows >= 10
* Connection timeout - related to the security group or firewall
  * If still an issue if fixed in AWS, then it might be a corporate firewall issue
* Connection refused - instance is running but no SSH server running
* Permission denied - Wrong security key, user, EC2 configuration
* ec2-user is the default user name

## EC2 Instance Connect

* Browser-based ssh connection
* Utility does all of the auto-magic key generation in the background
* Comes with AWS CLI
* Never enter KEYS in EC2, use IAM roles instead, attach it to the instance (the role)

## EC2 Instances Purchasing Options

* On-Demand Instances - short workload, predictable pricing, pay by second
* Reserved (1 & 3 years)
  * Reserved Instances - long workloads
  * Convertible Reserved Instances - long workloads with flexible instances
* Savings Plans (1 & 3 years) - commitment to an amount of usage, long workload
* Spot Instances - short workloads, cheap, can lose instances (less reliable)
* Dedicated Host - book an entire physical server, control instance placement
* Dedicated Instances - no other customers will share your hardware
* Capacity Reservations - reserve capacity in a specific AZ for any duration

### EC2 On Demand

* Pay for what you use:
  * Linux or Windows - billing per second, after the first minute
  * All other operating systems - billing per hour
* Highest cost, but no upfront payment
* No long-term commitment
* Recommended for short-term and un0interrupted workloads where you can't predict how the application will behave

### EC2 Reserved Instances

* Up to 72% discount compared to on-demand
* You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
* Reservation Period - 1 year (+discount) or 3 years (+++discount)
* Payment Options - No Upfront (+), Partial Upfront (++), All Upfront (+++)
* Reserved Instance's Scope - Regional or Zonal (reserve capacity in an AZ)
* Recommended for steady-state usage applications (think database)
* Buy or sell in the Reserved Instance Marketplace
* A "Convertible" Reserved Instances
  * Can change the EC2 instance type, instance family, OS, scope, and tenancy
  * Up to 66% discount

### EC2 Savings Plan

* Get a discount based on long-term usage (up to 72% - same as RIs)
* Commit to a certain type of usage ($10/hour for 1 or 3 years)
* Usage beyond EC2 savings plans is billed at the on-demand price
* Locked to a specific instance family & AWS region
* Flexible across:
  * Instance size
  * OS
  * Tenacy (host, dedicated, default)

### EC2 Spot Instances

* Get a discount of up to 90% compared to on-demand
* Instances that you can "lose" at any point of imte if your max price is less than the current spot price
* MOST cost-efficient instances in AWS
* Useful for workloads that are resilient to failure
  * Batch jobs
  * Data analysis
  * Image processing
  * Any distributed workloads
  * Workloads with a flexible start and end time
* Not suitable for critical jobs or databases

### EC2 Dedicated Hosts

* A physical server with EC2 instance capacity fully dedicated to your use
* Allows you to address compliance requirements and use your existing server-bound software licenses (per core, per socket, etc.)
* Purchasing options
  * On-demand - pay per second for active dedicated host
  * Reserved - 1 or 3 years (no upfront, partial upfron, all upfront)
* The most expensive option
* Useful for software that has complicated licensing model
* Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances

* Instances run on hardware that's dedicated to you
* May share hardware with other instances in the same account
* No control over instance placement
  * Can move hardware after Stop / Start

### EC2 Capacity Reservations

* Reserve On-Demand instnaces capacity in a specific AZ for any duration
* You always have access to EC2 capacity when you need it
* No time commitment (create/cancel anytime), no billing discounts
* Combine with Regtional Reserved Instances and Savings Plans to benefit from billing discounts
* You're charged at On-Demand rate whether you run instances or not
* Suitable for short-term, uniterrupted workloads that need to be in a specific AZ

### Which Purchasing Option Is Right for Me?

* On demand: coming and staying resort whenever we like, we pay the full price
* Reserved: like planning ahead and if we plan to stay for al ong time, we may get a good discount
* Savings Plans: pay a certain amount per hour for a certain period and stay in any room type (suite, sea view, ...)
* Spot instances: the hotel allows people to bid for the empty rooms and the higest bidder keeps the rooms. You can get kicked out at any time.
* Dedicated hosts: we book an entire building of the resort
* Capacity reservations: you book a room for a period with a full price even if you don't stay in it

## Shared Responsibility

### AWS Responsible

* Infrastructure (global network security)
* Isolation on physical hosts
* Replacing faulty hardware
* Compliance validation

### User Responsible

* Security group rules
* OS patches and updates
* SW and utilities installed on the EC2 instance
* IAM roles and access management
* Data security

## Summary

* EC2 Instance: AMI (OS) + Instance Size (CUP + RAM) + Storage + security groups + EC2 user data
* Security Groups: firewall attached to the ec2 instance
* EC2 User Data: script launched at the first start of an instance
* SSH: start a terminal into our EC2 instances (port 22)
* EC2 Instance Role: link to IAM roles
* Purchasing Options: On-Emand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance,

## Quiz

Good job, dude.


## References
