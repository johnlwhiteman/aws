# 07: ELB & ASG - Elastic Load Balancing & Auto Scaling Group

## High Availability, Scalability, Elasticity

* Scalability means that an application / system can handle greater loads by adapting
* Two kinds of scalability:
  * Vertical Scalability
  * Horizontal Scalability (elasticity)
* Scalability is linked but different to High Availability

### Vertical Scalability

* Vertical Scalbility means increasing the size of the instance
  * For example, your application runs on a t2.micro
  * Scaling that application vertically means running it on a t2.large
* Vertical scalability is very common for non-distributed systems, such as a database
* There's usually a limit to how much you can vertically scale (hardware limit)

### Horizontal Scalability

* Horizontal Scalability means increasing the number of instances / systems for your application
* Horizontal scaling implies distributed systems
* This is very comomon for web applications / modern applications
* Easy to hoizontally scale thanks to the cloud offerings such as EC2

### High Availability (HA)

* HA usually goes hand in hand with horizontal scaling
* HA means running your application / system in at least 2 AZs

### High Availability and Scalability for EC2

* Vertical Scaling: Increase instance size (= scale up / down)
  * From t2 to 12tb ...
* Horizontal Scaling: Increase number of instances (= scale out / in)
  * Auto Scaling Group
  * Load Balancer
* High Availability: Run instance for the same application across multi AZ
  * Auto Scaling Group multi AZ
  * Load balancer in multi AZ

## Scalability vs Elasticity vs Agility

* Scalability: ability to accomodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
* Elasticity: once a system is scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friendly": pay-per=use, match demand, optimize costs
* Agility: (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes

## Elastic Load Balancing (ELB) Overview

* Load balancers are servers that forward internet traffic to multiple servers (EC2 instances) downstream
* Why use it?:
  * Spread load across multiple downstream instances
  * Expose a singe point of access (DNS) to your application
  * Seamlessly handle failures of downstream instances
  * Do regular health checks to your instances
  * Provide SSL termination (HTTPS) for your websites
  * HA across AZs
* ELB (Elastic Load Balancer) is a managed load balancer
  * AWS guarantees that it will be working
  * AWS takes care of upgrades, maintenance, high availability
  * AWS provides only a few ocnfiguration knobs
* It costs less to setup your own load balancer but it will be a lot more effort on your end (maintenance, integrations)
* Four kinds of load balancers offered by AWS:
  1. Application Load Balancer (ALB) (HTTP/HTTPS only) - Layer 7
  2. Network Load Balancer (NLB) (ultra-high performance, allows for TCP) - Layer 4
  3. Gateway Load Balancer (GWLB) - Layer 3
  4. Classic Load Balancer (retired in 2023) - Layer 4 & 7

### Application Load Balancer (ALB)

* HTTP/HTTPS / gRPC protocols (Layer 7)
* HTTP Routing Feature
* Statifc DNS (URL)

### Network Load Balancer (NLB)

* TCP / UDP protocols (Layer 4)
* High performance: millions of requests per second
* Static IP through Elastic IP

### Gateway Load Balancer (GWLB)

* Uses GENEVE protocol on IP packets (layer 3)
* Route traffic to firewalls that you manage on EC2 instances
* Intrustion detection
* Sends to 3rd party security for virtual appliances

## Auto Scaling Groups (ASG) Overview

* In real-life, the load on your websites and applications can change
* In the cloud, you can create and get rid of servers very quickly
* The goal of an Auto Scaling Group (ASG) is to:
  * Scale out (add EC2 instances) to match an increased load
  * Scale in (remove EC2 instances) to match a decreased load
  * Ensure we have a minimum and a maximum number of machines running
  * Automatically register new instances to a load balancer
  * Replace unhealthy instances
* Cost savings: only run at an optimal capacity (principle of the cloud)
* Parameters
  * Minimum size
  * Actual size / desired capactiy
  * Maximum size
* Works hand-in-hand with a load balancer
* Create a launch template

## Auto Scaling Groups (ASG) Strategies

* Manual Scaling
  * Update the size of an ASG manually
* Dynamic Scaling: Respond to changing demand
  * Simple / Step Scaling
    * When a CloudWatch alarm is triggered (example CPU > 70%) then add 2 units
    * When a CloudWatch alarm is triggered (example CPU < 30%) then remove 1 unit
* Target Tracking Scaling
  * Example: I want the average ASG CPU to stay at around 40%
* Scheduled Scaling
  * Anticipate a scaling based on known usage patterns
  * Example: increase capacity to 10 at 5 pm on Fridays
* Predictive Scaling
  * Use Machine Learning to predict future traffic ahead of time
  * Automatically provision the right number of EC2 instances in advance
  * Useful when your load has predictable time-based patterns

## ELB and ASG Summary

* High Availability vs Scalability (vertical and horizontal) vs Elasticity vs Agility in the Cloud
* Elastic Load Balancers (ELB)
  * Distribute traffic across backend EC2 instances, can be Multi-AZ
  * Supports health checks
   * Four types
     1. Classic (old)
     2. Application (L7)
     3. Network (TCP/UDP L4)
     4. Gateway (L3)
* Auto Scaling Groups (ASG)
  * Implement Elasticity for your application across multiple AZ
  * Scale EC2 instances based on the demand on your system, replace unhealthy
  * Integrated with the ELB

## Quiz

* Application thriving even in case of a disaster is the main purpose of HA in the Cloud?
* An Auto Scaling Group (ASG) can automatically and quickly scale-in and scale-out to match the changing load on your applications and websites.
* Auto Scaling Groups can add or remove instances, but from the same type. They cannot change the EC2 Instances Types on the fly.
* Auto Scaling Strategies include: Manual Scaling, Dynamic Scaling (Simple/Step Scaling, Target Tracking Scaling, Scheduled Scaling), and Predictive Scaling.
* Auto Scaling Groups (ASG) offers the capacity to scale-out and scale-in by adding or removing instances based on demand.
* Load Balancers cannot help with back-end autoscaling. You should use Auto Scaling Groups.

## References