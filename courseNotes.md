# Cloud Practitioner Certification notes
Armando Mercado November 2023

AWS Regions
 - AWS has Regions all around the world
 - Names can be us-east-1, eu-west-3...
 - A region is a cluster of data centers
 - Most AWS service are region scoped
  
How to choose an AWS Region
 - Compliance with data governance and legal requirements
 - Proximity to customers
 - Available Services
 - Pricing
  
AWS Availability Zones
 - Each region hast many availability zones (usually 3, min is 3, max is 6)
 - Each availability zone is one or more discrete data centers ith redundant power, networking, and connectivity
 - They're separate from each other, isolated from disasters
 - They're connected with high bandwidth, low latency networking

## Exam Cloud Computing Quiz #1
q) You ONLY want to manage Applications and Data. Which type of Cloud Computing model should you use? Platform as a Service

q) Which of the following is NOT an advantage of Cloud Computing? Train your employees less

## IAM Section - Summary
 - Users: Mapped to a physical user, has a password for AWS console
 - Groups: Contains users only
 - Policies: JSON document that outlines permissions for users or groups
 - Roles: for EC2 instances or AWS services
 - Security: MFA + Password Policy
 - AWS CLI: Command line management
 - AWS SDK: Programming language management
 - Access keys: CLI or SDK access

IAM Credentials report is an IAM Security Tool
IAM Users NEVER access AWS with the root account credentials
AWS Customer is responsible for proper assigning of IAM Policies

## EC2 Section
EC2 is one of the most popular AWS Services
 - EC2 = Elastic Compute Cloud (Infrastructure as a service)
  
EC2's Capabilities: 
 - Renting virtual machines (EC2)
 - Storing data on virtual drives (EBS)
 - Distributing load across machines (ELB)
 - Scaling the services using an auto-scaling group (ASG)

EC2 Congifuration options
 - Operating System
 - Compute power CPU
 - memory RAM
 - Storage (EBS for network, Instance Store for hardware)
 - Network card (Speed of the card)
 - Firewall rules
 - Bootstrap script

EC2 Instances Purchasing Options
 - On-demand instances - Short workload, predictable pricing, pay by second
 - Reserved (1 & 3 years)
 - Savings Plans (1 & 3 years) - Commitment to an amount of usage, long worload
 - Spot Instances - Short workloads, cheap, can lose instances
 - Dedicated Hosts - book an entire physical server, control instance placement
 - Dedicated instances - no other customers will share your hardware 
 - Capacity Reservations - reserve capacity in a specific AZ for any duration

### Summary

Which EC2 Purchasing Option can provide the biggest discount, but is not suitable for critical jobs or databases? Spot Instances

Under the Shared Responsibility Model, who is responsible for operating-system patches and updates on EC2 Instances? The customer

How long can you reserve an EC2 Reserved Instance? 1 or 3 years

## EC2 - EBS Section
Think of it as a "Network USB"
- An EBS (Elastic Block Store) volume is a network drive you can attach to your instances while they run
- It allos your instances to persist data, even after their termination
- They can only be mounted to one instance at a time (at the CCP level)
- They are bound to a specific availability zone

### EBS Volume
- It's a network drive (uses the network to communicate the instance)
- It can be detached from an EC2 Instance and attached to another one quickly
- It´s locked to an Availability Zone (Need a snapshot to move it to another AZ)
- Have A provisioned capacity (GBs and IOPS) and you can increase the capacity of the drive over time

### EBS Delete on Termination attribute
- Controls the EBS behaviour when an EC2 Instance terminates
- By default, the root EBS volume is deleted
- by default, any other attached EBS volume is not deleted
- This can be controlled by the aws console / AWS CLI
- Use case: preserve root volume when instance is terminated

### FSx overview
- Launch 3rd party high-performance file systems on AWS
- Fully managed service
  
FSx for windows file server
  - A fully managed, highly reliable and scalable Windows native shared file system
  - Built on windows file server
  - supports SMB protocol & windows NFTS
  - Integrated with microsoft active directory
  - can be accessed from AWS or your on-premise infrastructure
  
FSx for Lustre
- A fully managed, high-performance, scalable file storage for High Performance Computing (HPC)
- The name lustre is derived from "Linux" and "cluster"
- Machine Learning, Analytics, Video Processing, Financial Modeling,...
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## Elastic Load Balancing & Auto Scaling groups
- Scalability means that an application / system can handle greater loads by adapting
- There are two kinds of scalability
  - Vertical Scalability
  - Horizontal Scalability (Elasticity)
- Scalability is linked but different to High Availability

### Vertical Scalability 
- Vertical scalability means increasing the size of the instance
- From junior operator to senior operator
- Vertical scalability is very common for a non distributed system, such as database
- There's a hardware limit

### Horizontal Scalability
- Horizontal Scalability means increasing the number of instances / systems for your application
- From 1 junior operator to 6 junior operators
- Distributed systems
- this is very common for web application / modern applications
- It's easy to horizontally scale thanks the cloud offerings such as Amazon EC2
  
### High Availability
- High Availability usually goes hand in hand with horizontal scaling
- High availability means running your application / system in at least 2 availability zones
- The goal is to survive a disaster

Scalability vs Elasticity vs Agility
- Scalability: ability to accommodate a larger load by making the hardware stronger or by adding nodes
- Elasticity: Once a system is scalable, elasticity means that will be "auto-scaling" so that the system can scale base on the load, this is cloud-friendly
- Agility (distractor) : new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

## S3 Section
Overview
  - Amazon S3 is one of the main building blocks of AWS
  - It's advertised as "infinitely scaling" storage
  - Many websites use Amazon S3 as a backbone
  - Many AWS services use Amazon S3 as an integration as well

Use Cases
- Backup and storage
- Disaster recovery
- Archive
- Hybrid Cloud Storage
- Application hosting
- Media hosting
- Data lakes & big data analytics
- Software delivery
- Static website

### Buckets
- Allows to store objects (files) in "buckets" (directories)
- Buckets must have a globally unique name
- Buckets are defined at the region level
- S3 looks like a global service but buckets are created in a region
- Naming Convention
  - No uppercase, no underscore
  - 3-63 characters long
  - Not an IP
  - Must start with lowercase letter or nomber
  - Must NOT start with the prefix xn--
  - Must NOT end with the suffix -s3alias

### Objects
- Objects (files) have a key
- the key is the full path:
  - s3://my-bucket/my_file.txt
  - s3://my-bucket/my_folder1/another_folder/my_file.txt
- The key is composed of prefix + object name 
- There's no concept of "directories" within buckets (although the UI will trick you to think otherwise)
- Object maximum size is 5TB, if is bigger use "multi-part upload".
- Metadata (list of key/ value pairs)
- Tags (unicode key/value pair, up to 10)
- Version ID (if versioning is enabled)

### Security
- User based
  - IAM Policies - Which API calls should be allowed for a specific user from IAM
- Resource Based
  - Bucket Policies - bucket wide rules from the S3 console -allows cross account
  - Object Access Control List (ACL) - finer grain (can be disabled)
  - Bucket Access Control List (ACL) - less common (can be disabled)
- Note: an IAM principal can access S3 object if:
  - The user IAM permissions ALLOW it or the resource policy ALLOWS it 
  - AND there's no explicit DENY
- Encryption: encrypt objects in Amazon S3 using encryption keys
  
S3 Bucket Policies
- JSON based policies
  - Resources: buckets and objects
  - Effect: Allow / Deny
  - Actions: Set of API to Allow or Deny
  - Principal: The account or user to apply the policy to
- Use s3 Bucket for policy to:
  - Grant public access to the bucket
  - Force objects to be encrypted at upload
  - Grant access to another account (Cross Account)

### Static Website Hosting
- S3 can host static websites and hace them accessible on the internet
- The website URL will be :
  - http://**bucket-name**.s3-website-**aws-region**.amazonaws.com
- If you get a **403 Forbidden** error, make sure the bucket policy allows public reads.

### Versioning
- You can version your files in Amazon S3
- It is enabled at the bucket level
- Same key overwrite will change the version : 1,2,3...
- It is best practice to version your buckets
  - Protect against unitended deletes (ability to restore a version)
  - Easy roll back to previous version
- Notes
  - Any file that is not versioned prior to enabling versioning will have version "null"
  - Suspending versioning does not delete previous versions

### Replication (CRR & SRR)
- Must enable versioning in source and destination buckets
- **Cross-Region Replication (CRR)**
- **Same-Region Replication (SRR)**
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3
- Use Cases:
  - **CRR** - compliance, lower latency access, replication across accounts
  - **SRR** - log aggregation, live replication between production and test accounts

### S3 Storage Classes
Durability and Availability
- Durability:
  - High durability (99.999999999%, 11 9's) of objects across multiple AZ
  - If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
  - Same for all storage classes
- Availability:
  - Measures how readily available a service is
  - Varies depending on storage class
  - Example: S3 standard has 99.99% availability = not available 53 minutes a year

Classes

- Amazon S3 Standard - General Purpose
  - 99.99% Availability
  - Used for frequently accessed data
  - Low latency and high throughput
  - Sustain 2 concurrent facility failures
  - **Use Cases**: Big Data analytics, mobile & gaming applications, content distribution...
  
- Amazon S3 Standard-Infrequent Access (IA)
  - 99.9% Availability
  - For data that is less frequently accessed, but requires rapid access when needed
  - Lower cost than S3 Standard
  - **Use cases**: Disaster Recovery, backups
- Amazon S3 One Zone-Infrequent Access
  - High durability (99.999999999%) in a single AZ
  - Data lost when AZ is destroyed
  - 99.5% Availability
  - **Use Cases**: Storing secondary backup copies of on-premise data, or data you can recreate
- Amazon S3 Glacier Instant Retrieval
  - Low-cost object storage meant for archiving / backup
  - Pricing: price for storage + object retrieval cost
  - Milisecond retrieval, great for data accessed once a quarter
  - Minimum storage duration of 90 days
- Amazon S3 Glacier Flexible Retrieval
  - Expedited (1 to 5 minutes), standard (3 to 5 hours), bulk (5 to 12 hours) - free
  - Minimum storage duration of 90 days
- Amazon S3 Glacier Deep Archive
  - Standard (12 hours), bulk (48 hours)
  - Minimum storage duration of 180 days
- Amazon S3 Intelligent Tiering
  - Small monthly monitoring and auto-tiering fee
  - Moves objects automatically between Access Tiers based on usage
  - There are no retrieval charges in S3 Intelligent-Tiering
  - Frequent Access tier (automatic): default tier
  - Infrecuent Access tier (automatic): objects not accessed for 30 days
  - Archive Instant Access tier (automatic): objects not accessed for 90 days
  - Archive Access tier (optional): configurable from 90 days to 700+ days
  - Deep Archive Access tier (optional): configurable from 180 days to 700+ days
  
Can move between classes manually or using S3 Lifecycle configurations.

AWS Snow Family - for Data migrations
 - Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS
 - Data Migration:
   - Snowcone
     - Small, portable computing, anywhere, rugged & secure
     - Light 4.5 pounds, 2.1kg
     - Device used for edge computing, storage, and data transfer
     - Snowcone - 8TB of HDD storage
     - Snowcone SDD - 14TB of SSD storage
     - Use snowcone where snowbal does not fit
     - Must provide your own battery / cables
     - Can be sent back to AWS offline, or connect it to internet and use AWS DataSync to send data
   - Snowball
     - Physical data transport solution, move TBs or PBs of data in or out AWS
     - Alternative to moving data over the network
     - Pay per data transfer job
     - Storage Optimized
       - 80TB of HDD capacity for block volume 
     - Compute Optimized
       - 42TB of HDD or 28TB NVMe capacity for block volume
     - Large cloud migrations, disaster recovery
   - Snowmobile
     - An actual trol LMAO
     - Exabytes of data (1,000 PB)
     - High security: temperature controlled, GPS, 24/7 video surveillance
     - Better than Snowball if you transfer more than 10PB
 - Edge Computing: 
   - Snowball
   - Snowcone
     - Process data while its being created on an edge location
     - These locations may have limited / no internet access
     - No access to computing power
     - Machine learning at the edge
     - Transcoding media streams
     - Ship back to AWS if needed
 - AWS OpsHub
   - Software management tool for Snow Family Device

PAY FOR EVERYTHING EXCEPT FOR DATA INTO AWS

EXAM NOTES:
Which S3 Storage Class is the most cost-effective for archiving data with no retrieval time requirement? **Amazon Glacier Deep Archive**

A research team deployed in a location with low-internet connection would like to move 5 TBs of data to the Cloud. Which service can it use? **Snowcone**

A non-profit organization needs to regularly transfer petabytes of data to the cloud and to have access to local computing capacity. Which service can help with this task? Snowball **Edge - Storage Optimized**

## Code Deployment & Managing infraestructure

Cloud formation : terraform but aws

CDK: terraform but for every programming language

Beanstalk: PaaS for applications and health monitoring metrics for instances

CodeDeploy: Applications to deploy automatically, Hybrid service 

CodeCommit: aws competing product to git.

CodeBuild: allows to build code in the Cloud compile, run test, and produces packages. Pay as you go

CodePipeline: Orchestrate the different steps to have the code pushed to production Basis for CI/CD

CodeArtifact: is a secure artifact management for software development (works with dependency management tools) Stores code dependecies

CodeStar: Unified easily manage software development activities in one place, quick way for all the code stack

Cloud9: AWS Cloud IDE, collaboration and reviews from anywhere.

SSM: Manages EC2 and On-premises systems at scale, hybrid service, way to patch all instances

SSM Session Manager: Allows to start a secure shell for ec2 instances, no ssh (no port 22)

SSM parameter Store: Secure storage for configuration and secrets ( vault )

OpsWorks: Alternative to SSM and we can only provide standard resources (chef and puppet) to reuse previous configurations

## Global Infraestructure

An application deployed in multiple geographies

- less latency

- Disaster Recovery for availability

- Protection to attacks

Route 53: Managed DNS, manages trafic and makes health checks with weighted Routing policy

Cloud Front: CDN improves read performance improves user experience by cached content, DDoS protections

S3 Transfer Acceleration: increase transfer speed by transferring file to an aws edge location wich will forward the data to the s3 bucket in the region

AWS Global Accelerator: improves connection by levereaging the aws internal network (60% improvement)

AWS Outposts: Are server racks that offers the same AWS infrastructure to build applications just as in the cloud

AWS WaveLength: Infraestructure deployments ebedded with the telecommunications providers datacenters at the edge of the 5G networks

AWS Local Zones: Place AWS Instances closer to end users to run latency-sensitive applications

Single Region
Multiple Region Active Pasive
Multiple Region Active Active

## Cloud Integrations

Communications
- Syncronous
- Async / Event based

SQS Simple que service:
- Producers send messages into the que and poll the messages to the consumer
- Serverless service
- FIFO Queue to send messages in order

Kinesis: real time big data streaming, colect process and analyze real-time streaming data at any scale
- Streams: low latency streaming to ingest data at scale
- Firehouse: load streams into S3,Redshift, ElasticSearch, etc...
- Analitycs: Perform real-time analytics on streams using SQL
- Video Streams: monitor real-time video streams for analytics or ML

SNS Simple Notification Service 
- sends message into the sns and the consumers get nottificated by the topic (message brokers)

Amazon MQ: Alternative to on-premisses to not use SNS and SQS (message broker)

## Cloud Monitoring

EventBridge (Cloudwatch events)
- Schedule cron jobs (scripts)
- Event rules to react to
- Trigger other services

CloudTrail
- Enabled by default
- governance, compliance and audit for aws account
- output to cloudwatch logs or s3 bucket

AWS Xray
- Debugginf tool to trace and give visual analysis of our applications
- Troubleshooting performance
- find errors and review request behavior
- where stuff is happening
- identifies users affected
  
Amazon CodeGuru
- Code reviews and appplication performance recommendations. MachineLearning powered service
- Supports Java and Python
- Profiler understand runtime behavior of application
  
AWS Healt Dashboard
- Shows all regions all services health.
- Shows historical information for each day
- Your Account gives alerts and remediation guidance when aws is experiencing events that may impact you
  
## VPC & Networking
Virtual Private Cloud

Main Cloud Practitioner Concepts
- VPC, Subnets, Internet Gateways & NAT Gateways
- Security Groups, Network ACL (NACL), VPC Flow Logs
- VPC Peering, VPC Endpoints
- Site to Site VPN & Direct Connect
- Transit Gateway

IP Addresses in AWS
- IPv4 4.3 Billion Addresses
  - Ec2 instances gets a new public ip every time you stop then start it
  - Private IPv4 can be used on private networks such as internal AWS Networking
  - Private IPv4 is fixed for EC2 Instances even if you start/stop them
- Elastic IP
  - Allows to Attach a fixed public IPv4 address to EC2 isntance
- IPv6  3.4 x 10**38 Addresses
  - Every IP is public

VPC & Subnets Primer
- VPC: private network to deploy your resources (regional resources)
- Subnets allow you to partition your network inside your VPC
- A public subnet is accessible from the internet
- To define access we use Route Tables
- Internet gateway helps our VPC instances connect with the internet
- Public Subnets have a route to the internet gateway
- Nat Gateways allows private instances connect to public internet keeping privacy 

NACL - subnet level
- A firewall which controls traffic from and to subnet
- Can have ALLOW and DENY rules
- Are attached at the subnet level
- Rules only include IP addresses
  
Security Groups - instance level
- A firewall that controls traffic to and from an ENI/EC2 instance
- can have only ALLOW rules
- Rules include IP addresses and other security groups

VPC Flow logs
- Capture information about IP traffic going into your interfaces
- Helps to monitor and troubleshoot connectivity issues

VPC peering
- Connect two VPC, privately using AWS's network
- Make them behave as if they were in the same network
- Must not have overlapping CIDR
- VPC peering is not transitive (must be established for each VPC that neet to communicate with one another)

VPC Endpoints
- Allow to connect to AWS services using a private network
- Gives enhanced security and lower latency to AWS services
- S3 & DynamoDB

PrivateLink
- Most secure & scalable way to expose a service to 1000s of VPCs
- Does not require peering, internet gateway or any config...
- Private link joins a producer network load balancer with a customer elastic network interface
  
Site to site VPN
- Connect on-premises VPN to AWS
- the connection is automatically encrypted
- goes over the public internet
  
DX
- Establish a physical connection between on premises and AWS
- The connection is private, secura and fast
- Goes over a private network
- Takes at leas a month to establish
  
Client VPN
- Connect from your computer using OpenVPN to your private network in AWS and on-premises
- Allow to connect EC2 instances over a private IP
  
Transit Gateway 
- for having transitive peering between thousands of VPC and on-premises, hub-and-spoke connection
- one single gateway to provide this functionality
- works with DX and VPN connections


  
