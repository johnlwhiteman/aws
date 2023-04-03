# 10: Other Compute Services: ECS, Lambda, Batch, Lightsail

## What is Docker?

* Docker is SW development plantform to deply apps
* Apps are packaged in containers that can be run on any OS
* Apps run the same, regardless of where they're run
  * Any machine
  * No cmpatibility issues
  * Predictable behavior
  * Less work
  * Easier to maintain and deploy
  * Works with any language, any OS, any technology
* Scale containers up and down very quickly (seconds)
* Where Docker images are stored in Docker respositories
* Public: Docker Hub https://hub.docker.com
  * Find base images for many technologies or OS
  * Ubuntu
  * MySQL
  * NodeJS, Java ...
* Private: Amazon ECR (Elastic Container Registry)
* Docker is "sort of" a virtualization technology but not exactly
* Resources are shared with the host => many containers on one server

## ECS, Fargate & ECR Overview

###  Elastic Container Service (ECS)

* ECS = Elastic Container Service
* Launch Docker containers on AWS
* You must provision and maintain the infrastructure (the EC2 instances)
* AWS takes care of starting/stopping containers
* Has integrations with the Application Load Balancer

### Fargate

* Launch Docker containers on AWS
* You do not have to provision the infrastructure
* NO EC2 instances to manage ... simpler!
* Serverless offering
* AWS just runs containers for you based on the CPU / RAM you need

### Elastic Container Register (ECR)

* Elastic container registry
* Private Docker Registry on AWS
* This is where you store your Docker images so they can be run by ECS or Fargate

## Serverless Introduction

* Serverless is a new paradigm in which the developers don't have to manage servers anymore
* They just deply code
* They just deploy ... functions!
* Initially ... serverless == FaaS (Function as a Service)
* Serverless was poineered by AWS Lambda but now also includes anything that's managed: "databases, messaging, storage, etc."
* Serverless does not mean there are no servers ... it means that you just don't manage / provision / see them
  * Amazon S3
  * DynamoDB
  * Fargate
  * Lambda

### Lambda Overview

#### EC2
* Virtual Servers in the Cloud
* Limited by RAM and CPU
* Continously running
* Scaling means intervention to add /remove servers

#### Lambda
* Virtual functions - no servers to manage
* Limited by time - short executions
* Run on-demand
* Scaling is automated

* Benefits
  * Pay per request and compute time
  * Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
  * Integrated with the whole AWS suite of services
  * Event-Driven: functions get invoked by AWS when needed
  * Integrated with many programming languages
  * Easy monitoring through AWS CloudWatch
  * Easy to get more resources per functions (up to 10GB of RAM)
  * Increasing RAM will also improve CPU and network

### AWS Lambda Language Support

* Node.js (JavaScript)
* Python
* Java (Java 8 compatible)
* C# (.NET Core)
* Golang
* C# / Powershell
* Ruby
* Custom Runtime API (community supported, example Rust)
* Lambda Container Image
  * The container image must implement the Lambda Runtime API
* Lambda pricing is based on calls and duration

## API Gateway Overview

* Example: Building a serverless API
* Fully managed service for developres to easily create, publish, maintain, monitor, and secure APIs
* Serverless and scalable
* Supports RESTful APIs and WebSocket APIs
* Support for security, user authentication, API throttling, API keys, monitoring

## Batch Overview

* Fully managed batch processing at any scale
* Efficiently run 100,000s of computing batch jobs on AWS
* A "batch" job is a job with a start and an end (opposed to continuous)
* Batch will dynamically launch EC2 instances or Spot Instances
* AWS Batch provisions the right amount of compute / memory
* You submit or schedule batch jobs and AWS Batch does the rest
* Batch jobs are defined as Docker images and run on ECS
* Helpful for cost optimizations and focusing less on the infrastructure

### Batch vs. Lambda

#### Lambda

* Time limit
* Limited languages/runtimes
* Limited temporary disk space
* Serverless


### Batch

* No time limit
* Any runtime as long as it's packaged as a Docker image
* Rely on EBS / instance store for disk space
* Relies on EC2 (can be managed by AWS)

## Lightsail Overview

* Virtual servers, storage, databases, and networking
* Low and predictable pricing
* Simpler alternative to using EC2, RDS, ELB, EBS, Route 53 ...
* Great for people with little cloud experience
* Can setup notifications and monitoring of your Lightsail resources
* Uses cases:
  * Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js ...)
  * Websites (templates for WordPress, magento, Plesk, Joomla)
  * Dev / Test environment
* Has high availability but no auto-scaling, limited AWS integrations

## Other Compute - Summary

* Docker: container technology to run applications
* ECS: run Docker containers on EC2 instances
* Fargate:
  * Run Docker containers without provisioning the infrastructure
  * Serverless offering (no EC instances)
* ECR: Private Docker Images Repository
* Batch: run batch jobs on AWS across managed EC2 instances
* Lightsail: predictable and low pricing for simple applications and DB stacks

### Lambda Summary

* Lambda is Serverless, Funcation as a Service (FaaS), seamless scaling, reactive
* Lambda Billing
  * By the time run x by the RAM provisioned
  * By the number of invocations
* Language Support: many programming languages except (arbitrary) Docker
* Invocation time: up to 15 minutes
* use Cases:
  * Create thumbnails for images uploaded onto S3
  * Run a serverless cron job
* API Gateway: expose Lambda functions as HTTP API

## Quiz

How do you get charged in AWS Lambda? In AWS Lambda, you are charged per request and compute time, that's it.

You would like to launch Docker containers in AWS without worrying about provisioning or managing any infrastructure. The Docker containers will be used to host a heavy workloads to serve different types of requests. Some requests may need up to 30 minutes to be completed. Which AWS service should you use to run Docker containers in a Serverless way and satisfy the requirements? Fargate allows you to launch Docker containers on AWS, and you don't need to provision and maintain the infrastructure (=no EC2 instances to manage). It is Serverless.

A complete cloud beginner would like to create a simple application with predictable pricing. What service should this person use? Amazon Lightsail is designed to be the easiest way to launch and manage a virtual private server with AWS. Lightsail plans include everything you need to jumpstart your project – a virtual machine, SSD- based storage, data transfer, DNS management, and a static IP address – for a low, predictable price. It can be used to create a simple web application, a website or a dev/test environment.

What is the name of the software development platform that allows you to run applications the same way, regardless of where they are run? Docker is a software development platform that allows you to run applications the same way, regardless of where they are run. It can scale containers up and down within seconds.

How would you best describe "event-driven" in AWS Lambda? "Event-driven" in Lambda means that functions are invoked when needed. They are triggered.

Which AWS service allows you to launch Docker containers on AWS, but requires you to provision and maintain the infrastructure? ECS allows you to launch Docker containers on AWS, but you must provision and maintain the infrastructure (i.e. EC2 instances).

Which of the following statements is INCORRECT regarding the definition of the term "serverless"? Serverless does not mean that there are no servers, you just do not manage, provision and see them, but they do exist.

Which of the following statements is NOT a feature of AWS Lambda? This is a feature of Auto Scaling Groups, not AWS Lambda.

A company needs to run thousands of jobs but would like to NOT manage the compute resources. What service can it use? AWS Batch enables developers, scientists, and engineers to easily and efficiently run hundreds of thousands of batch computing jobs on AWS. AWS Batch dynamically provisions the optimal quantity and type of compute resources (e.g., CPU or memory-optimized instances) based on the volume and specific resource requirements of the batch jobs submitted.

Where should you store your private Docker images so they can be run by ECS or Fargate? Elastic Container Registry (ECR) is a service where you store your Docker image so they can be run by ECS or Fargate.

Which AWS serverless service can be used by developers to create APIs? success alert
Good job!
Amazon API Gateway is a fully managed serverless service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale.

## References