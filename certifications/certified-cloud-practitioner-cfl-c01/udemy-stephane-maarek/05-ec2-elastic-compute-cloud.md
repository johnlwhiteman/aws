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

## SSH Overview

* Linux / Max / Windows >= 10



## References
