# 03: What Is Cloud Computing


## What is Cloud Computing

* On-demand delivery of compute power, database storage, applications, and other IT resources
* Pay-as-you-go pricing
* Provision exactly right type and size of computing resources
* Access all resources instantly
* Simple way to access resources
* AWS owns the systems

### Private Cloud

* Used by a single organization, not exposed to the public
* Complete control - the customer has
* Security for sensitive applications
* Meet specific business needs

### Public Cloud

* Cloud resources owned and operated by a third-party cloud service provider delivered over the Internet
* Six Advantages of Cloud Computing

### Hybrid Cloud

* Keep some servers on premises and extend some capabilities to the Cloud
* Control over sensitive assets in your private infrastructure

### Five Characteristics of Cloud Computing

1. On-demand self service
  * Users can provision their own resources
2. Broad network access
  * Resources available over the network, and can be accessed by diverse client platforms
3. Multi-tenancy and resource pooling
  * Multiple customers can share the same infrastructure and applications with security and privacy
  * Multiple customers are serviced from the same physical resources
4. Rapid elasticity and scalability
  * Automatically and quickly acquire and dispose resources when needed
  * Quickly and easily scale based on demand
5. Measured service
  * Usage is measured, users pay correctly for what they have used

## Six Advantages of Cloud Computing

1. Trade capital expense (CAPEX) for operational expense (OPEX)
  * Pay on-demand, don't own hardware
  * Reduced total cost of ownership (TCO) and operational expense (OPEX)
2. Benefit from massive economies of scale
  * Prices are reduced as AWS is more efficient due to large scale
3. Stop guessing capacity
  * Scale based on actual measured usage
4. Increase speed and agility
5. Stop spending money running and maintaining data centers
6. Go global in minutes: leverage the AWS global infrastructure

## Problems Solved by the Cloud

* Flexibility
* Cost-effective
* Scalability
* Elastic
* High-availability and fault tolerance
* Agility

## The Different Types of Cloud Computing

* Infrastructure as a Service (IaaS)
  * Provide building blocks for cloud IT
  * Provides networking, computers, data storage space
  * Highest level of flexibility
  * Easy parallel with traditional on-premises IT
  * Amazon EC2 (on AWS), GCP, Azure, Rackspace, Digital Ocean, Linode

* Platform as a Service (PaaS)
  * Remove the need for your organization to manage the underlying infrastructure
  * Focus on the deployment and management of your applications
  * Elastic Beanstalk, Heroku, Google App Engine (GCP), Windows Azure (MS)

* Software as a Service (SaaS)
  * Completed product that is run and managed by the service provider
  * Rekognition for ML, Google Apps, Dropbox, Zoom

### Pricing of the Cloud - Quick Overview

* AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model

1. Compute
  * Pay for compute time
2. Storage
  * Pay for data stored in the cloud
3. Networking
  * Pay for only data leaving the cloud

![responsibilities](images/responsibilities.png(

## AWS Cloud Overview

* 2002 AWS internally launched
* 2004 SQS first public offering

### AWS Regions

* AWS has Regions all around the world
  * us-east-1, eu-west-3, ...
* Cluster of data centers
* Most AWS services are region-scoped
* Factors that impact choosing a region:
  * Compliance
  * Latency / Proximity
  * Available services - not all regions provide the same services
  * Pricing - does vary from region to region

### AWS Availability Zones

* Each region has many availability zones, usually 3 up to 6 max
  * ap-southeast-2a, ap-southeast-2b, ap-southeast-2c
* Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity
* AZs are separated from each other so that they can isolate from disasters
* Connected with high bandwidth, ultra-low latency networking

### AWS Points of Presence (Edge Locations)

* Amazon has 216 Points of Presence (205 edge locations and 11 regional caches) in 84 cities across 42 countries
* Content is delivered to end users with lower latency

### AWS Global Services

* Identity and Access Management (IAM)
* Route 53 (DNS Service)
* CloudFront (Content Delivery Network)
* WAF (Web Application Firewall)


### AWS Region Services

* Most services will be region-scoped
* EC2, Elastic Beanstalk, Lambda, Rekognition
* https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/

## Quiz

* You ONLY want to manage Applications and Data. Which type of Cloud Computing model should you use? 
  * (PaaS)
* What is the pricing model of Cloud Computing?
  * Pay-as-you-go pricing
* Which Global Infrastructure identity is composed of one or more discrete data centers with redundant power, networking, and connectivity, and are used to deploy infrastructure?
  * Availability zones
* Which of the following is NOT one of the Five Characteristics of Cloud Computing?
  * Dedicated support agent to help you deploy applications
* Which are the 3 pricing fundamentals of the AWS cloud
  * Compute, Storage, Data transfer out of the AWS Cloud
* Which of the following options is NOT a point of consideration when choosing an AWS Region?
  * Capacity availability
* Which of the following is NOT an advantage of Cloud Computing?
  * Train your employees less
* AWS Regions are composed of?
  * Two or more Availability Zones
* Which of the following services has a global scope?
  * IAM
* Which of the following is the definition of Cloud Computing?
  * On-demand availability of computer system resources, especially data storage (cloud storage) and computing power, without direct active management by the user
* What defines the distribution of responsibilities for security in the AWS Cloud?
  * The Shared Responsibility Model
* A company would like to benefit from the advantages of the Public Cloud but would like to keep sensitive assets in its own infrastructure. Which deployment model should the company use?
  * Hybrid Cloud
* What is NOT authorized to do on AWS according to the AWS Acceptable Use Policy?
  * Run analytics on stolen content


## References

* https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/
