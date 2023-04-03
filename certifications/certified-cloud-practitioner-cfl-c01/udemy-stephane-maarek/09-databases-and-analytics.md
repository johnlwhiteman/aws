# 09: Databases and Analytics

## Database Intro

* Storing data on disk (EFS, EBS, EC2, Instance Store, S3) can have its limits
* Sometimes, you want to store data in a database
* You can structure the data
* You build indexes to effiently query / search through the data
* You define relationships between your datasets
* Database are optimized for a purpose and come with different features, shapes, and constraints
* SQL DBs
* NoSQL DBs
  * JSON

### Databases & Shared Responsibility on AWS

* AWS offers use to manage different databases
* Benefits include:
  * Quick provisioning, HA, vertical, and horizontal scaling
  * Automated backup & restore, operations, upgrages
  * OS patching is handled by AWS
  * Monitoring and alerting
* Note: Many database technologies could be run on EC2, but you must handle yourself with resiliency, backup, patching, high availability, fault tolerance, scaling, ...

## RDS & Aurora Overview

* RDS stands for Relational Database Services
* It's managed DB service for DB use SQL as a query language
* It allows you to create databases in the cloud that are managed by AWS
  * Postgres
  * MySQL
  * MariaDB
  * Oracle
  * Microsoft SQL Server
  * Aurora (AWS Proprietary Database)

### Advantage over using RDS versu deplying DB on EC2

* RDS is a managed service:
  * Automated provisioning, OS Patching
  * Continuous backups and restore to specific timestamp (Point in Time Restore)
  * Monitoring dashboards
  * Read replicas for improved read performance
  * Multi AZ setup for DR (Disaster Recovery)
  * Maintenace windows for upgrades
  * Scaling capability (vertical and horizontal)
  * Storage backed by EBS (gp2 or iol)
* BUT you can't SSH into your instances

### RDS Solution Architecture

                        / [EC2 Instance]
[Elastic Load Balancer] - [EC2 Instance]  ->  [RDS]
                        \ [EC2 Instance]

### Aurora Architectures

* Amazon Aurora is a proprietary technology from AWS (not open sourced)
* PostgreSQl and MySQL are both supported as Aurora DB
* Aurora is "AWS cloud optimized" and claims 5x performance improvements over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 128 TB
* Aurora costs more than RDS (20% more) - but is more efficient
* Not in the free tier

## RDS Deployments Options

* Read Replicas:
  * Scale the read workload of your DB
  * Makes DB copies ... can create up to 15 Read Replicas
  * Writing is done with the main DB only
* Multi-AZ:
  * Failover in case of AZ outage (high availability)
  * A failover DB will be crated
  * If main DB crashes, then the failover DB will take over

### RDS Deployments: Multi Region

* Multi-Region (Read Replicas)
  * Disaster recovery in case of region issue
  * Local performance for global reads
  * Replication cost

## ElastiCache Overview (in memory)

* The same way RDS is to get managed RDs
* ElastiCache is to get managed Redis or Memcached
* Caches are in-memory dbs with high performance, low latency
* Helps reduce load off dbs for read intensive workloads
* AWS takes care of OS maintenace / patching, optimizations, setup, configuration, monitoring, failure recovery, and backups

## DynamoDB Overview (NoSQL)(Serverless)(Low Latency)

* Fully managed, highly available with replication across 3 AZs
* NoSQL DB - not a relational db
* Scales to massive workloads, distributed "serverless" database
* Millions of requests per second, trillions of rows, 100s of TB of storage
* Fast and consistent in performance
* Single-digit millisecond latency - low latency retrieval
* Integrated with IAM for security, authorization, and adminstration
* Low cost and auto scaling capabilities
* Standard and infrequent access (IA) table class
* Key/value database
  * Primary Key
    * Partition key
    * Sort Key

### DynamoDB Accelerator - DAX

* Full managed in-memory cache for DynamoDB
* 10x performance improvement - single-digit millisecond latency to microseconds latency - when accessing your DynamoDB tables
* Secure, highly scalable, and high available
* Difference with ElastiCache at the CCP level: DAX is only used for an is integrated with DynamoDB, whil ElastiCache can be used for other databases

## DynamoDB Global Tables

* Make a DynamoDB table accessible with low latency in multiple-regions
* Two-way replication (r/w) access to any region in the world

## Redshift Overview (OLAP)

* Based on PostgeSQL, but it's not used for OLTP
* It's for OLAP - online analytical processing (analytics and data warehousing)
* Load data once every hour, not every second
* 10x better performance than other data warehouses, scales to PBs of data
* Columnar storage of data (instead of row based)
* Massively Parallel Query Execution (MPP), highly available
* Pay as you go based on the instances provisioned
* Has a SQL interface for performing queries
* Business Intelligence (BI) tools such as AWS Quicksight or Tableau integrate with it

## EMR Overview (Hadoop)

* Elastic MapReduce
* EMR helps create Hadoop Clusters (Big Data) to analyze and process vast amounts of data
* Clusters can be made of hundreds of EC2 instances
* Also supports Apache Spark, HBase, Presto, Flink, ...
* EMR takes care of all the provisioning and configuration
* Auto-scaling and integrated with Spot instances
* Use cases: data processing, machine learning, web indexing, big data, ...

## Athena Overview (Serverless BI)

* Serverless query service to perform analytics against S3 objects
* Uses standard SQl language to query the files
* Supports CSV, JSON, ORC, Avro, and parquet (built on Presto)
* Pricing: $500 per TB of data scanned
* Use compressed or columnar data for cost-savings (less scan)
* Use cases: Business intelligences / analytics/ report analyze, and query VPC flow logs, ELB logs, CloudTrail trails, etc...

**Exam Tip: Analyze data in S3 using serverless SQL, use Athena**

## QuickSight Overview

* Serverless machine learning-powered business intelligence service to create interactive dashboards
* Fast, automatically scalable, embeddable wit hper session pricing
* Use cases:
  * Business analytics
  * Building visualizations
  * Perform ad-hoc analysis
  * Get business insights using data
* Integrated with RDS, Aurora, Athena,  Redshift, S3, ...

## DocumentDB Overview (NoSQL -> MongoDB)

* Aurora is an "AWS-implementation" of PostgreSQL / MySQL ...
* DocumentDB is the same for MongoDB (which is a NoSQL DB)
* MongoDB is used to store, query, and index JSON data
* Similar "deployment concepts" as Aurora
* Fully managed, high available with replication across 3 AZ
* DocumentDB storage automatically grows in increments of 10GB, up to 64TB
* Automatically scales to workloads with millions of requests per seconds

## Neptune Overview (a graph db)

* Fully managed graph database
* Popular graph dataset would be a social network
  * Users have firends
  * Posts have comments
  * Comments have likes from users
  * Users share and like posts
* Highly available across 3 AZ, with up to 15 read replicas
* Build and run applications working with highly connected datasets - optimized for these complex and hard queries
* Can store up to billions of relations and query the graph with milliseconds latency
* Highly available with replications across multiple AZs
* Great for knowledge graphs (Wikipedia), fraud detection, recommendation engines, social engineering

## QLDB Overview (finance)

* QLDB stands for "Quantum Ledger Database"
* A ledger is a book recording financial transactions
* Fully managed, serverless, high available, replication across 3 AZ
* Used to review history of all the changes made to your applicatio ndata over time
* Immutable system: no entry can be removed or modified, cryptographically verifiable
  * Hashing
* 2-3x better performance than common ledger blockchain frameworks, manipulates data using SQL
* Differences with Aamzon Managed Blockchain: no decentralization component, in accordance with financial regulation rules

## Managed Blockchain Overview

* Blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority
* Amazon Managed Blockchain is a managed service to:
  * Join public blockchain networks
  * Or create your own scalable private network
* Compatible with the frameworks Hyperledger Fabric, and Ethereum

## Glue Overview

* Managed extract, transform, and load (ETL) service
* Useful to prepare and transform data for analytics
* Fully serverless service
* Glue Data Catalog: catalog of datasets
  * Can be used by Athena, Redshift, EMR

## Database Migration Service (DMS) Overview

* Quickly and securely migrate databases to AWS, resilient, self healing
* Source database remains available during the migration
* Supports:
  * Homogeneous migrations: Oracle to Oracle
  * Heterogeneous migrations: Microsoft SQL Server to Aurora

## Databases & Analytics Summary

* Relational Databases - OLTP: RDS and Aurora (SQL)
* Differences between Multi-AZ, Read Replicas, Multi-Region
* In-memory Database: ElastiCache
* Key/Value Database: DynamoDB (Serverless) and DAX (Cache for DynamoDB)
* Warehouse - OLAP: Redshift (SQL)
* Hadoop Cluster: EMR
* Athena: Query data on Amazon S3 (Serverless and SQL)
* QuickSight: Dashboards on your datas (Serverless)
* DocumentDB: "Aurora for MongoDB" (JSON - NoSQL database)
* Amazon QLDB: Financial Transactions Ledger (centralized, immutable journal, cryptographically verifiable)
* Amazon Managed Blockchain: managed Hyperledger Fabric & Ethereum blockchains
* Glue: Managed ETL (Extract Transform Load) and Data Catalog service
* Database migration: DMS
* Neptune: graph database

## Quiz

You want to create a decentralized blockchain on AWS. Which AWS service would you use? Amazon Managed Blockchain is a fully managed service that makes it easy to create and manage scalable blockchain networks using the popular open source frameworks Hyperledger Fabric and Ethereum. It allows multiple parties to execute transactions without the need of a trusted, central authority.

Which AWS database is a data warehouse? Amazon Redshift is a fully managed, petabyte-scale data warehouse service in the cloud.

Which AWS service is always serverless and has SQL capabilities? Amazon Athena is an interactive query service that makes it easy to analyze data in Amazon S3 using standard SQL. Athena is serverless, so there is no infrastructure to manage, and you pay only for the queries that you run.

You would like to use a serverless service to prepare data so it can be loaded for analytics. Which service would you use? AWS Glue is a fully managed extract, transform, and load (ETL) service that makes it easy for customers to prepare and load their data for analytics.

Which relational database is a proprietary technology from AWS and is cloud-optimized? Amazon Aurora is a MySQL and PostgreSQL-compatible relational database built for the cloud, that combines the performance and availability of traditional enterprise databases with the simplicity and cost-effectiveness of open source databases. It is a proprietary technology from AWS.

You would like to migrate databases to AWS while still being able to use the database during the migration. What service allows you to do this? AWS Database Migration Service helps you migrate databases to AWS quickly and securely. The source database remains fully operational during the migration, minimizing downtime to applications that rely on the database.

How can you create Hadoop clusters to analyze and process a vast amount of data? Amazon EMR is a web service that enables businesses, researchers, data analysts, and developers to easily and cost-effectively process vast amounts of data. EMR helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data

Which in-memory AWS database can you use to reduce the load off databases and has high performance, low latency? Amazon ElastiCache is a web service that makes it easy to deploy and run Memcached or Redis protocol-compliant server nodes in the cloud. ElastiCache caches are in-memory databases with high performance, low latency. They help reduce load off databases for read intensive workloads.

What is the name of a central repository to store structural and operational metadata for data assets in AWS Glue? The AWS Glue Data Catalog is a central repository to store structural and operational metadata for all your data assets. For a given data set, you can store its table definition, physical location, add business relevant attributes, as well as track how this data has changed over time.

Which of the following databases is a managed service with SQL capability suited for Online Transaction Processing (OLTP)? Amazon Relational Database Service (Amazon RDS) is a SQL managed service that makes it easy to set up, operate, and scale a relational database in the cloud. It is suited for OLTP workloads

Which AWS service is an immutable ledger database? Amazon QLDB is a fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log owned by a central trusted authority. Amazon QLDB tracks each and every application data change and maintains a complete and verifiable history of changes over time.

You would like to set up a NoSQL database that can scale with no downtime and can handle millions of requests per second. Which AWS database is best suited for this work? DynamoDB is a fast and flexible non-relational database service for any scale. It can scale with no downtime, it can process millions of requests per second, and is fast and consistent in performance.

Which AWS service can create complex graphs for fraud detection? Amazon Neptune is a fast, reliable, fully-managed graph database service that makes it easy to build and run applications that work with highly connected datasets. It can be used for knowledge graphs, fraud detection, recommendations engines, social networking, etc.

Which AWS serverless service can use machine learning-powered business intelligence to create interactive dashboards such as business analytics? Amazon QuickSight is a fast, cloud-powered business intelligence (BI) service that makes it easy for you to deliver insights to everyone in your organization. You can create and publish interactive dashboards.

A company would like to set up a fully managed MongoDB database. Which AWS database is best-suited for this task? Amazon DocumentDB (with MongoDB compatibility) is a fast, calable, highly available, and fully managed document database service that supports MongoDB workloads.

Which exclusive DynamoDB feature is an in-memory cache that can improve your performance up to 10x? Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for Amazon DynamoDB that delivers up to a 10 times performance improvement—from milliseconds to microseconds—even at millions of requests per second.

RDS Multi-AZ deployments’ main purpose is high availability, while RDS Read replicas’ main purpose is scalability. RDS Multi-AZ deployments’ main purpose is high availability, and RDS Read replicas’ main purpose is scalability. Moreover, Multi-Region deployments’ main purpose is disaster recovery and local performance.

## References
