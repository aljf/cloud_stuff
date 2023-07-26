# AWS Cloud Practitioner

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1fdff9a-8392-49b0-b22b-75fcc4ebde75/Untitled.png)

IaaS

- Deploy most of the infra yourself
- Easily flexible but more work
- Ex: AWS EC2

PaaS

- Remove need for org to maintain infra
- focus now on dev and development of apps
- Ex: Elastic Beanstalk

SaaS

- Completed product
- run and managed by service provider
- Ex: many AWS apps

## Pricing of Cloud

Pay-as-you-go

Compute

- pay as you compute

Storage

- pay for data stored in cloud

For Data transfer **OUT** of cloud

- Data transfer IN cloud = **free**

How to choose AWS region

- Compliance
- Proximity
- Available Services
    - Not all features are in every region

Shared Responsibility Model

Customer = responsible for security IN the cloud

AWS = security OF the cloud

# IAM

## Users & Groups

**Root acct** created by default don’t use or share 

**Users** are people within your organization and can be grouped 

**Groups** only have other users not other groups

Users doesn’t have to be in a group or can be added to multiple groups

## Permissions

Users can be assigned with JSON = policies

## IAM Policies

inline policy = 1 persion policy

role policy = group policy 

consists of:

“statement” required 

“Effect”: allow or deny access

“action”

## IAM Password Policy

strong password = more security

In AWS can set:

- min password length
- require specific character types
- Require user to change password after some time

## Multi Factor Authentication - MFA

users have access to your acct and can possibly change configurations or delete resources in your AWS acct

You want to protect your Root Accts and IAM Users 

## MFA Options on AWS

Virtual MFA: Authy, Google Authenticator

Universal 2nd Factor: Yubikey 

Hardware Key Fob MFA 

 

## AWS Access

to access aws from 3 options:

- AWS Mgmt console
- AWS CLI
- AWS SDK
- Access are generated through the AWS console
- Access keys = secret

## AWS CLI

tool to enable you to interact with AWS services using command line 

direct access to public APIs

## AWS SDK

- Language-specific aPIs
- enable access/manage AWS services programmatically
- 

 

## IAM Roles for Services

- Some AWS services will need permissions to do some actions
- The service needs IAM permissions to do this

## IAM Security Tools

- IAM Credentials Report (acct-lvl)
    - report that list all acct’s users and status of multiple creds
- IAM Access Advisor (usr-lvl)
    - Access Advisor shows the service permission granted to a user and when those services were last accessed
    - use info to revise policies

## Responsibility Model for IAM

AWS is responsible for:

- Infra
- Configuration and vuln analysis
- Compliance validation

You are responsible for:

- User, groups, policies mgmt and monitoring
- enable MFA on all accts
- rotate all keys often
- Analyze access patterns and review permission

## EC2 - Elastic Compute Cloud

EC2 is most popular AWS service

IaaS as a Service = EC2

consists of:

- rent VMs - EC2
- storing data on virtual drives - EBS
- Distributing load across machines - ELB
- Scale services using auto-scaling group - ASG

Ec2 sizes and config options

- OS: Linux, Windows, or Mac OS
- CPU
- RAM
- How much storage
    - Network attached
    - hardware
- Network card: speed of card
- Firewall rules: security group
- Bootstrap script

EC2 User Data

- Bootstrap our instances using EC2 user data script
- bootstrapping = launch cmds when machine starts
    - only runs once on first start
- Usually things like:
    - install updates
    - install software
    - download files on internet
    - anything
- script runs with root user

EC2 instance types basics

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b8010d7-315d-4b8e-9132-a8f28e6d08ab/Untitled.png)

- General purpose
    - good for diversity of workloads
    - balance between
        - compute
        - memory
        - networking
- compute optimized
    - great for compute-intensive tasks req. high perf. processors
        - Batch processing
        - media transcoding
        - high perf. web servers
- Memory optimized
    - fast perf. for procesing large data sets in memory
    - Use cases
        - High perf. rela/non-relat dbs
        - dist. web scale cache stores
- Storage Optimized
    - great for storage-intensive tasks that require high, seq. read and write access to large data sets on local storage

## Security Groups & Classic ports Overview

- Security Groups are the fundamental of network security in AWS
- control how traffic is allowed into or out of our EC2 instances
- Security groups only contain allow rules
- security groups rules can ref by IP or by security group

Deep Dive

- Sec groups are acting as “firewall” on Ec2 instances
- regulates
    - access to ports
    - authorized Ip ranges
    - control of inbound network
    - control of outbound network

Security group con’t

- can attach to multiple instances
- locked down to a regiion /VPC connection
- does live “outside” the EC2 - if traffic is blocked the Ec2 instance won’t see it
- its good to maintain one separate security group for SSH access
- all inbound is blocked by default
- all outbound is allowed by default

Classic ports to know

22 = SSH - log into linux instances

21 FTP - upload file using into file share

22 = SFTP - upload file share using SSH

80 = HTTP

443 = HTTPS

3389 = RDP - log into windows machine 

SSH Summary Table

SSH = Mac, Linux, and Windows 10 or greater

Putty = All Windows Versions

EC2 Instance connect = works for everything 

EC2 Instances Purchasing Options 

- On-demand instances - short workload, predictable pricing, pay by sec
- Reserved ( 1 & 3 years)
    - Reserved Instances - long workloads
    - Convertible Reserved instances - long workloads with flexible instances
    - Reserves specific instance attributes - large discount
    - Regional or zonal
    - good for dbs, steady-state usage
- Savings plans (1 & 3 years)
    - commit to amount of usage, for long workloads
    - large discount
    - commit to cetrain type of usage
    - locked into specific instance family
        - but flexible with
            - instance size
            - OS
            - tendency
- Spot instances - short workloads, cheap, can lose instances
    - you can lose at any point of time if your max price is less than the current spot price
    - Most cost-efficient instances in AWS
    - Useful for workloads resilient to failure
    - Not suited for critical apps
- Dedicated hosts - book an entire physical server, control instance placement
    - physical server w/ Ec2 instance capacity fully dedicated to your use
    - allow you address compliance req. and use your existing server-bound software licenses
    - most expensive option
    - good for software with complicated licensing model  or company with strong regulatory/compliance needs
- Dedicated instances - no other customers will share your hardware
    - run on hardware dedicated to you
    - may share hardware with other instances in same acct
    - no control over instance placement
- capacity reservations - reserve storage in a specific AZ
    - Reserve on-demand instances capacity in a specific AZ for any duration
    - you always have access to EC2 capacity when you need it
    - no time commitment (cancel anytime), no billing discounts
    - combine w/ regional reserved instanaces and savings plans to benefit from billing discounts
    - you’re charged at on-demand rate whether you run instances or not

## Shared Responsibility Model for EC2

Aws responsible for:

- infra
- isolation on physical hosts
- replacing faulty hardware
- compliance validation

You’re responsible for:

security group rules

OS patches and updates

Software and utilities installed 

## EBS Overview

EBS = Elastic block store = network drive you can attach to your instance while they run 

- allow instance to presist data even after termination
- mount 1 instance at a time
- like “network USB stick”

## EBS Volume

- network drive
    - communicate to instance so might have latency
    - detach from one EC2 to another quick
- Locked to 1 AZ
    - to move AZ make snapshot
- Have provisioned capacity
    - billed for all provisioned capacity
    - increase capacity of drive over time

## EBS - delete on termination attribute

- when you create a EBS you can add flag
- turned on by default for root
- default other EBS is not deleted
- Use case: preserve root volume when instance is terminated - need to disable delete on termination flag

## EBS Snapshots

- make backup/snapshot of EBS volume at any point
- not necessary to detach volume to do snapshot but recommended
- can copy snapshots across AZ

## EBS Snapshots Features

- EBS Snapshot Archive
    - Move snapshot to an “archive tier” that is 75% cheaper
    - take w/i 24 to 72 hrs for restoring archive
- Recycle bin for EBS Snapshots
    - set up rules to retain deleted snapshots to protect against accidental deletion

## AMI Overview

AMI = Amazon Machine Image 

- AMI are customization of EC2 instance
    - you add your own software, config, OS, monitoring
    - Faster boot / config time bc all your software is pre-packaged
    - AMI are built for specific region
- you can launch EC2 instances from:
    - Public AMI: AWS provided
    - own AMI: make an maintain yourself
    - An AWS Marketplace AMI: AMI someone else made (and could sell)

## AMI Process (from EC2 instance)

- start an EC2 instace and customize it
- stop instance (for data integrity)
- Build an AMI - this will also create EBS snapshots
- Launch instances from other AMIs

## EC2 Image builder

- Used to automate creation of VMs or container images
- Automate the creation, maintain, validate and test **EC2 AMIs**
- can be run on a schedule
- free service (only pay for underlying resources)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/debda8b5-60eb-4db1-b245-2715d5502ba1/Untitled.png)

## EC2 Instance store

- EBS volumes are network drives w/ good but “limited” perf.
- If you need a high-perf. hardware disk , use EBS instance store
- Better I/o performance
- Ec2 instance store lose their storage if they’re stopped
- good for buffer / cache / temp content
- risk of data loss if hardware fails
- backups are your responsibility

## EFS - Elastic File System

- Managed NFS can be mounted to 100s of Ec2
- EFS works w/ linux EC2 instances in multi-AZ
- highly available, scalable, expensive, pay per use, no capacity planning (pay for how much you store)

## EBS vs EFS

- EBS: 1 AZ and only for 1 instance at one time; need snapshot to move to another AZ
- EFS: network drive that are shared by all instances mounted to it

## EFS infrequent Access

- storage class cost-optimized for files not accessed every day
- up to 92% lower cost compared to EFS std.
- EFS auto move files to EFS-IA based on last time they were accessed
- enabled EFS-IA w/ lifecycle policy
- ex: move files not accessed for 60 days to EFS-IA

## Responsibility Model for EC2 Storage

AWS

- infra
- replication for data for EBS vol. and EFS drives
- replace faulty hardware
- ensure employees cannot access your data

Your resp.

- setting up backup
- setting up data encryption
- data on drives
- risk of data loss Ec2 instance store

## Amazon FSx — Overview

- Launch 3rd party high-perf. file sys. on AWS
- fully managed service

## FSx for Windows File Server

- fully managed Windows native shared file sys.
- built on Windows File Server
- Support SMB & NFTS
- integrated w/ AD
- can be accessed on AWS or on own infra

## FSx for Lustre

- high perf. computing file storage
- Lustre = linux, cluster
- Use cases: ML, video processing, fin modeling

# Elastic Load Balancing & Auto Scaling Groups

## Scalability & High availability

- Scability = app /sys. can handle greater loads by adapting
- 2 kinds:
    - vertical
    - horizontal
- Scability is linked but different to high availability

## Vertical scalability

- means **increasing the size of instance**
- ex: app run on t2.micro to t2.large
- vertical scale very common for non distributed sys.
- there is a hardware limit

## Horizontal Scalability

- **increase # of instances** for your app
- horizontal scaling implies distributed sys.
- very common web app
- easy to scale w/ Auto scaling groups & load balancer

## High Availability

- usually goes hand in hand w/ horiz. scale
- high avail means **running in at least 2 AZ**
- Goal: survive a disaster

Scalability vs Elasticity vs Agility

- scalability: ability to accommodate a large load by making the hardware strong or add nodes
- elasticity: once sys is scalable means auto-scaling so sys. can scale based on load
- agility: distractor

## Elastic Load Balancer Overview

- load balancers are servers that forward internet traffic to multiple servers downstream
- spread load across multiple instances
- expose single point of DNS to your app
- seamlessly handle failures of downstream instances
- SSL termination feature for websites
- high availability across zones

Why use ELB?

- managed load balancer
    - AWS guarantee it will work
    - AWS does all upgrades, maintainence, high avail
    - AWS provide only few config knobs
- cost less to setup your own but will be more effort and maintenance
- 4 kind of load balancers
    - Application Load Balancer - Layer 7 HTTP
    - Network Load Balancer (ultra high perf.) Layer 4 TCP
    - Gateway Load Balancer - Layer 3
    - Classic (Old)
- Differences

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ecde0fc3-af10-410e-8af1-cc07994b8ba8/Untitled.png)

## Auto Scaling Groups

- why
    - real-life load on websites change with time
    - in cloud you can create and get rid of servers very quickly
    - goal of Auto Scaling Group is to:
        - Scale out
        - Scale in
        - Ensure we have min and max # of machines running
        - Auto register new instances to a load balancer
        - replace unhealthy instances
    - Cost Savings: only run at an optimal capacity

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/329b318a-ec5a-494b-8902-f886801ba42f/Untitled.png)

ASG Group w/ load balancer 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a28701c-505e-44ba-8717-6d025090f7b9/Untitled.png)

ASGs - Scaling Strats

- Manual Scaling: update size ASG manually
- Dynamic Scaling
    - Simple / step scaling
        - Ex: when cloudwatch alarm is triggered then add 2 units
        - when CPU < 30% then remove 1
    - Target tracking scaling
        - Ex: I want the avg. ASG CPU to stay around 40%
    - Scheduled Scaling
        - Anticipate a scaling based on know usage
        - Ex: increase capacity on Friday evening
- Predictive Scaling
    - use ML to predict future traffic ahead of time
    - auto provision the right # of EC2 instances
    - Useful when your load has predictable time-based patterns

# AWS S3

## Introduction

- S3 = “infinitely scaling” storage
- Many websites use S3

## Use Cases

- Backup & Storage
- Disaster Recovery
- Archive
- Hybrid Cloud Storage
- App Hosting
- Media Hosting
- Data lake & big data analytics
- Software delivery
- Static website

S3 - buckets

- S3 to store obj. in buckets
- buckets must have globally unique names (across all regions all accts)
- buckets defined on region level
- S3 look like gloabl serivce but regional

## S3 - objects

- obj have a key
- key is FULL path
- key is composed of prefix+ obj. name
- no concept of “directories” w/i buckets
- just keys w/ very long names that contain slashes
- obj. values are content of the body
    - max obj. size = 5TB
    - if upload > 5 GB use “multi-part upload”

- Metadata (list of key /value pairs of usr metadata)
- Tags
- Version ID

## S3 - Security

- usr-based
    - IAm policies - which API calls allows for specific user from IAM
- Resource-based
    - bucket policies - bucket wide rules from S3 console - allows cross acct
    - Obj. access control list - finer grain
    - Bucket ACL - less common
- Note: IAM principal can access S3 obj. if
    - user IAM permissions ALLOW OR resource policy ALLOWS it
    - AND there’s no explicit deny
- Encryption: encrypt obj with keys

## Bucket policies

- JSon based policies
    - resources: buckets and objs.
    - effect: allow / deny
    - actions: set of API to allow or deny
    - principal: acct or usr to apply the policy to
- Use S3 bucket for policy to:
    - grant public access to bucket
    - force obj. to be encrypted on upload
    - grant access to another acct.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63a33896-e221-456e-b0d1-923d510f9b3b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f85f055-ffd0-4e17-be4b-93ef2b55a8ba/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0363df00-4baf-423d-b521-47e2bc6e939a/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a19b3e58-e4f7-46af-ab0c-59ac4faa4b90/Untitled.png)

## Bucket settings for block public access

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da212bc4-069e-44bd-bf1a-b701c03ee83d/Untitled.png)

- these settings were created to prevent company data leaks

## S3 - static website hosting

- s3 can host static websites
- if you get 403 error make sure bucket policy allows public reads

## S3 - versioning

- version files in S3
- enabled at bucket lvl
- same key overwrite will change the “version”: 1,2,3
- best practice to version your buckets
    - protect against unintended deletes (restore a version)
    - easy roll back to previous version
- Notes:
    - any file not versioned prior to versioning will be set to “null”
    - suspending versioning does not delete previous versions

## s3 - replication

- must enable versioning in source and dest. buckets
- Cross-Region Replication
- Same-Region Replication
- buckets can be in different AWS accts
- copy is async
- must give proper IAM permissions to s3
- Use cases
    - CRR - compliance, lower latency access, replication across accts
    - SRR - log aggreg., live replication btwn production and test accts

## s3 storage classes

- s3 std. - General purpose
- s3 std.-Infrequent access
- s3 1 zone-infreq access
- …
- can move between classes manually or using s3 lifecycle configuration

## s3 durability and availability

- durability
    - how often you will lose a object
    - high durability
- availability
    - measure how readily available a service is
    

## S3 - general purpose

- 99.99% availability
- use for frequently accessed data
- low latency & high throughput
- sustain 2 concurrent facility failures

## s3 - infrequent access

- for data that is less frequently accessed, but requires rapid access when needed
- lower cost than s3 std
- s3 one zone-IA

s3 glacier storage classes

- low cost obj storage meant for archive / backup
- pricing: price for storage + obj. retrieval cost
- s3 glacier instant retrieval
    - ms retrieval, great for data accessed once a quarter
    - min storage duration of 90 days
- s3 glacier flexible retrieval
    - expedited (1-5 mins)
    - std (3-5 hrs)
    - bulk (5-12 hrs)
    - min storage duration of 90 days
- s3 glacier deep archive - for long term storage
    - storage (12 hrs)
    - bulk (48 hrs)
    - min storage duration of 180 days

## s3 intelligent-tiering

- small monthly monitoring and auto-tiering fee
- move obj auto between access tiers based on usage
- no retrieval charges in s3 intelligent-tiering

- freq. access tier
- infreq. access tier
- archive instant access tier
- …

## s3 encryption

- server-side encryption (default)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1c04117-a9b8-4e15-836a-1b14de07efc8/Untitled.png)

- Client-side encryption

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6e6f0826-0d47-499e-93c1-c99374779bff/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77fdd740-afc0-4c00-a665-c860dc191118/Untitled.png)

## AWS SNOW family

- highly-secure, portable devices to **collect and process data at the edge, and migrate data into and out of AWS**
- data migration
    - Snowcone
    - Snowball edge
    - Snowmobile
- edge computing
    - snowcone
    - snowball edge

Data migration w/ AWS Snow family

- Challenges
    - long data transfer time over network
    - limited connectivity
    - limited bandwidth
    - high network cost
    - shared bandwidth
- Snow family: offline devices to perform data migrations

Diagram 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8434334c-f091-4977-aa0a-c9dc8a66797a/Untitled.png)

## Snowball edge (data transfer)

- move TBs or PBs of data in or out of AWS
- alternatives to moving data over the network
- pay per data transfer job
- provide block storage & amazon s3-compatible obj. storage
- Snowball edge storage optimized
    - 80 TB of HDD capacity for block volume & s3 compatible obj. storage
- Snowball edge compute optimized
    - 42 TB of HDD

Snowcone & snowcone SSD

- small, portable computing, anywhere, rugged & secure
- light
- device used for edge computing, storage, and data transfer
- snowcone - 8 TB of HDD storage
- Snowcone SSD - 14 TB of SSD storage
- use snowcone where snowball does not fit
- must have own battery/ cables
- can send to AWS datasync service at a data center or send directly to AWS

Snowmobile

- Transfer exabytes of data

Summary 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3eff0eb1-6927-4d20-a691-7f087bffe894/Untitled.png)

## What is edge computing

- process data whie it’s being created on edge location
    - truck on road, a ship on sea, mining station
- these locations may have no internet but need computing
- Use cases
    - preprocess data
    - ML at edge
- Eventually ship back to AWS

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38a11b04-32c2-409b-98f3-1d172ef56be4/Untitled.png)

## AWS OpsHub

- software GUI for Snow family device to help with functions

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7c1785ae-4a5a-475c-94f7-97a847403bd5/Untitled.png)

## Hybrid Cloud for Storage

- AWS pushing for “hybrid cloud”
    - part of your infra is no-premises
    - part of your infra is on cloud
- This can be due to
    - long cloud migrations
    - security reqs.
    - compliance reqs.
    - IT strategy
- s3 is proprietary storage tech, so how to expose s3 data on premise?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f2640732-ea3a-4811-8a77-77c4bb23f630/Untitled.png)

## AWS Storage Gateway

- bridge between on-premise data and cloud data in S3
- hybrid storage service to allow on-premises to use AWS cloud
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06be4ac0-906c-403c-92b9-334d202a3556/Untitled.png)

# Databases

Intro

- storing on disk can have limits
- sometimes want to store data on db

## Relational Databases

- looks like excel spreadsheet, with links btwn them
- can use sql lg to perform queries / lookups

## NoSQL Databases

- noSQL = non-SQL = non relational dbs
- NoSQL dbs are purpose built for specific data models and have flexible schemas for buildign modern apps
- Benefits
    - flexibility
    - scalability
    - high perf.
    - high functional

NoSQL data ex. JSON

- Data can be nested
- fields can be changed over time
- support new types: arrays, etc.

## Shared responsibility Dbs

- AWS offers use to manage different dbs
- benefits include
    - quick provisioning, high availability
    - automated backup & restore, ops, upgrades
    - OS patching is handled by AWS
    - monitoring, alerting
- Note: can use your own DB on EC2 but you are responsible for everything

## AWS RDS Overview

- RDS = Relational DB service
- managed DB service for DB use SQL as query lang. ,
- allow you to create db in cloud that are managed by AWS
- SQL service for OTLP

## Adv. of RDS over own DB on EC2

- RDS is managed service:
    - autoamted provisioning, OS patching
    - continous backups and restore
    - monitoring dashboards
    - read replica for improved read perf.
    - multi AZ setup
- BUT can’t SSH into your instances

## RDS Solution Architecture

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02363fb2-309a-4746-9652-8ad80a163abb/Untitled.png)

## Amazon Aurora

- not open-source
- PostgresSQL and MySQL supported on Aurora DB
- is cloud optimized and claims 5x perf. improvement over MySQL on RDS over 3x perf. of postgres on RDS
- Aurora storage auto grows in increments of 10GB
- Costs more than RDS but more efficient
- not in free tier

## RDS Deployment: Read Replicas, Multi-AZ

- Read replicas
    - Scale the read workload of your DB (increase read perf.)
    - can create up to 15 read replicas
    - Data write is only for main DB
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b327d97e-3f8a-4fe7-9c9a-23fcdd398598/Untitled.png)
    
- Multi-AZ
    - Failover in case of AZ outage (high avail.)
    - data can only read/write to main db
    - can only 1 AZ as failover
    - 
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1112ee90-a4f1-472a-aeb4-b4f8dc1c6b9a/Untitled.png)
    
    ## RDS Deployment: Multi-Region
    
    - Multi-region
        - Disaster Recovery in case of region issue
        - local perf. for global reads
        - replication cost
        - 
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/76308a14-c3ad-4b94-8d87-9a4aabdb5b4c/Untitled.png)
        
    
    ## Amazon ElastiCache Overview
    
    - in memory DB
    - same way RDS is to get managed Relational DBs
    - ElastiCache is to get managed Redis
    - Cache are in-memory dbs with high perf., low latency
    - helps reduce load off dbs for read intensive workloads
    - AWS take care of patching,, optimizations, backups, etc.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b19b8763-66ac-4193-b26d-6d445aa43061/Untitled.png)
    
    ## DynamoDB
    
- Fully Managed highly avail. w/ replication across 3 AZ
- **NoSQL db - not relational db**
- Scales to massive workloads, distributed “**serverless**” db
- **Single-digit ms latency - low latency retrieval**
- Integrated w/ IAM for security, auth and admin
- low cost & auto scaling
- std. & infreq. access table class

## DynamoDB - type of data

- key/value db
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e80e5cf-a152-4762-9c3e-34999e5b7c35/Untitled.png)

## DynamoDB Accel. - DAX

- fully managed in-memory cache
- 10x perf. improvement - microsec. retrieval
- **DAX is only used for and is integrated w/ DynamoDB**

## DynamoDB - Global Tables

- make dynamoDB table accessible w/ **low latency** in multiple regions
- Active-Active replication (r/w to any AWS region)

## RedShift - Overview

- based on Postgres, but not used for OLTP
- OLAP - **online analytical processing (analytics and data warehousing)**
- load data once every hr, not every sec
- 10x better perf. than other data warehouse, scale to PBs of Data
- columnar storage
- pay as you go based on instances provided
- sql interface for queries
- integrate w/ tablaeu

## EMR

- “Elastic MapReduce”
- helps creating Hadoop clusters to analyze and process vast amount of data
- clusters can be made of hundreds of EC2 instances
- takes care of all provisioning and config
- auto-scaling and integrate w/ spot instances

## Athena

- serverless query service to perform analytics against S3 objs.
- use std. SQL lang. to query the files
- pricing : $5 per TB of data scanned
- use cases: buz int.
- Exam tip: analyze s3 data using serverless SQL = Athena

## Quicksight

- serverless ML buz. int. to create interactive dashboards
- use case
    - buz analytics
    - building viz
    - perform ad-hoc analysis

## DocumentDB

- Aurora = AWS implementation of Postgres.
- DocumentDB is same as MongoDB (NoSQL db)
- MongoDB used to store query and index JSON data
- fully managed, replication up to 3 AZ
- auto grows
- auto scales to workload

## Amazon Neptune

- **fully managed graph db**
- high avail.
- optimized for complex and hard queries

## Amazon QLDB

- stands for “quantum ledger db”
- recording financial transactions
- **used to review history of all the changes made to your app data over time**
- immutable sys.: no entry can be removed or modified
- 2-3x perf. than common ledger blockchain
- diff w/ amazon managed blockchain: no decentralization component

## Amazon Managed Blockchain

- join public blockchain netowrks
- or create your own

## AWS Glue

- managed extract, transform, and load (ETL) service
- fully serverless

## DMS - Databased Migration Service

- quick and secure migrate db, self healing
- source db remains available during the migration
- supports:
    - homogenous migration: move from same tech dbs
    - heterogeneous migration
    

# Other computing servces: ECS, Lamdbda, Batch, LIghtsail

## ECS Section

## What is docker?

- software dev platform to deploy apps
- Apps are packaged in containers that can run on any OS
- apps run the same, regardless of where they’re run
    - any machine
    - no compatibility issues
    - predictable behavior
    - less work
    - easier to maintain and deploy
- Scale containers up and down very quick

run multiple tech on 1 EC2 instance:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/678b9264-1fe7-48d8-8e5a-2b3c09cfeb2e/Untitled.png)

Docker images are stored on Dockerhub &

Private: Amazon ECR

## Docker vs VMs

- docker is “sort of” virtualization
- resources are shared w/ the host ⇒ many containers on one server

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a427c52-7fab-4e1f-a818-7729cc23a869/Untitled.png)

## ECS

- ECS = Elastic Container Service
- Launch Docker continers on AWS
- must maintain infra yourself
- Exam: Docker containers on EC2 = ECS

## Fargate

- Launch docker cont. on AWS
- you do not provision infra - simpler
- serverless offering
- AWS runs contains based on your needs

## ECR

- elastic container registry
- private docker registry on AWS
- store your docker images so they can run by ECS or Fargate
- 

Exam: ECS vs Fargate vs ECR

## Serverless

- new paradigm - developers don’t manage servers anymore
- just deploy code
- just deploy functions
- Initially, Serverless == FaaS (function as a service)
- does not mean no servers just means you don’t provision/manage them

## Why AWS Lambda

- Virtual Server in cloud
- limited by RAM and CPU
- continously monitoring
- PRos of Lambda
    - virtual functions
    - limited by time - short execution
    - run on-demand

## Lambda Pricing

- easy pricing
    - pay per request and compute time
    - free tier 1 mil AWS lambda requests
- integrate w other services
- Event-Driven: functions invoked by AWS when needed

Lambda lang support 

- 
    - Exam: ECS /far gate is preferred for running arbitrary docker images
    

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cdaf82d6-2a3b-4847-8a37-7f9eb7313c79/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/012ca54a-610c-43da-94ce-c967132141a0/Untitled.png)

## Amazon API Gateway

- ex: building serverless API
    - want external clients to use API
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f72febb-6bf8-4bcf-bed8-489a158a08c1/Untitled.png)

- fully managed service for devs to easily create, publish, maintain, monitor, and secure APIs
- Serverless and scalable
- support rest apis
- support security, throttling, keys, etc.

## AWS Batch

- fully managed batch processing at any scale
- efficiently run 100k computing batch jobs on AWS
- batch job is a job w/ a start and end
- batch will dynamically launch EC2 instances or Spot Instances
- will provision the right compute / memory
- batch jobs can be docker images and run on ECS

## Batch vs Lambda

Lambda

- time limit
- limited runtimes
- limited temp disk space
- serverless

Batch

- no time limit
- any runtime as long as it’s packed as docker img
- rely on EBS / instance store for disk space
- relies on EC2

## Am Lightsail

- virtual servers, storage dbs, and networking
- low & predictable pricing
- good for ppl w little cloud experience
- use cases
    - simple web apps
    - websites
    - dev / test envs

Summary

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b3bc0ad9-26df-46d4-a519-6d2646c85a8c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1efdcc10-d6ef-436a-8590-d08300fa4255/Untitled.png)

# <insert the rests here>

## AWS OpsWorks

- chef & puppet help w/ server config. auto or repetitive actions
- Opsworks = managed chef & puppet
- alt to AWS SSM
- 

## Deployment - summary

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54ead350-9b79-415a-8e44-2e40a794fb6f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f38c1a91-19fa-4bcc-9fc1-dbc63b8d03e0/Untitled.png)

## Why make a global app?

- global app deployed to multiple regions
- on aws: could be regions and edge locs
- decrease latency
    - if hosted near to each region = reduce latency
- Disaster Recovery
    - if aws region goes down
    - you have fail-over to another region so app still work
- Attack protection: increase avail.

## Global AWS infra

- regions: for deploy app and infra
- avail. zones: made of multiple data center
- edge locs: for content delivery as close as possible to users

## Route 53 Overview

- managed DNS
- DNS = collection of rules and records help clients get to url
- in aws,
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3f718002-f502-4c7f-a5f9-f4e8c1964ee5/Untitled.png)
    
    ## Route 53 Routing Policies
    
    - need to know for exam
    - weighted routing policy
        - distribute traffic to each ec2 instance
    - latency routing policy
        - check loc. to redirect user to lower latency
    - failover routing policy
        - dns does health check on primary, if fail go to failover
    
    ## Cloudfront
    
    - CDN - Content Delivery Network
    - Improve read perf, content cached at edge
    - improve UX
    - DDoS protection (bc worldwide)
    
    Cloudfront - origins
    
    - s3 bucket
        - for dist. files and caching them at edge
        - enhanced sec. w/ cloudfront Origin Access Control
    - Custom origin (HTTP)
        - app LB
        - EC2 instance
        - any HTTP backend you want
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/89594659-eeb4-4d1f-a129-2cae0d306ce6/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cdf77b00-05c4-4413-b22c-1df49f99e652/Untitled.png)
    
    Cloudfront v S3 cross region replication
    
    - Cloudfront
        - Global edge network
        - files are cached for a TTL
        - great for static content that must have avail.
    - s3 cross region replication
        - must setup for each region you want
        - files updated real-time
        - read-only
        - great for dynamic content that needs avail. at low latency in few regions
    
    ## S3 transfer accel.
    
    - incr transfer speed by trans file to edge location which forward data to s3 bucket in target regoin
    - for download file far from you
    
    ## AWS Global Accel.
    
    - improve global app avail and perf. using AWS global network
    - leverage AWS network to optimize the route to your app
    - 
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45f6dde2-7aff-4858-a053-8e9ed4f89fb1/Untitled.png)
    
    AWS Global Accel. vs Cloudfront
    
    - both use aws global network and its edge loc around the world
    - both have ddos protection
    - cloudfront - CDN
        - improve perf.
        - serve at edge
    - global accel.
        - no caching, proxying packets at edge
    
    ## AWS Outposts
    
    - hybrid cloud - on prem infra and cloud infra.
    - two ways to deal w IT sys
        - one for aws cloud
        - one for on-prem
    - AWS Outpost are “server racks” offer same aws infra
    - AWS will setup and manage “Outposts racks”
    - you are resp. for outposts rack physical security
    - Benefits
        - low latency
        - local data processing
        - data residency
        - easier migration from on-prem to cloud
    
    ## AWS Wavelength
    
    - **Wavelength zones** embedded on 5G networks
    - traffic never leaves CSP network
    - no additional charges
    
    ## AWS Local Zones
    
    - places AWS services closer to end user to run latency-sensitive apps
    - extend VPC to more loc “ext to AWS region”

## global App Architecture

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/aa8e001f-a1fd-4bd7-baff-70c81b4ce11c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a77f1e98-a741-4586-8f3f-5bdf0d09ff31/Untitled.png)

## Cloud Integration - Intro

- if you have multiple apps need to communicate with each other
- need asynchronous services you make multiple apps
- 
- 

 

## SQS - Overview

- Simple queue service
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/491969cb-c2c1-4d26-a789-a466c4388e5a/Untitled.png)

- 

## SQS

- serverless, decouple apps
- messages are deleted after they’re read by consumers

## SQS decouple between app tiers

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/08ae6940-3225-4a38-875d-ed3be9631bf9/Untitled.png)

## SQS - FIFO queue

- first in, first out
- msg processed in order

## Kinesis

- Kinesis = real-time big data streaming
- managed service to collect, process, and analyze real-time streaming data at any scale

## SNS - Overview

- if you want to send 1 msg to many recievers
- intermediary to send msg to correct app

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/32f3b3b4-e171-453d-b5bc-0bcae86ff014/Untitled.png)

## Amazon SNS

- evt publishers” only send msg to 1 SNS topic
- as many “evt subscribers” as we want to listen to the SNS topic notifications
- each subs to topic will get all the msgs
- **no msg retention**

## Amazon MQ

- SQS, SNS are cloud-native services: proprietary protocols from AWS
- traditional app running from on-prem may use open protocols
- when migrating to cloud, instead of re-engineeering the app use SQS and SNS we can use Amazon MQ
- **MQ = managed msg broker service**
- Amazon MQ doesn’t scale as much
- MQ runs on servers, can run in multi-AZ w/ failover
- MQ has both queue feature and topic features

## Cloudwatch Metrics

- Cloudwatch provide metrics for every services in AWS
- Metric is a variable to monitor
- Metrics have timestamps
- Create CloudWatch metrics dashboard

Ex: Billing metric dashboard

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5aa7d8f4-5575-4fd9-b1f3-67395ec69dfc/Untitled.png)

- EC2 instances: CPU Utilization, status checks, network
    - default metric every 5 min
- EBS volumes: Disk read/writes
- S3 buckets: BucketSizeBytes, NumberOfObjects, AllRequests
- Billing: Total Estimated Charge
- Service limits: how much you’ve been using a service API
- custom metrics

## Cloudwatch Alarm

- alarm trigger notification on any metric
- examples
    - Auto scaling: incr or decre EC2 instances “desired” count
    - Ec2 actions: stop, start, etc

## Cloudwatch Logs

- CloudWatch collect logs from:
    - elastic beanstalk: collection of logs from app
    - ECS” collect from containers
    - lambda: coll from func logs
    - **CloudWatch logs agents: EC2 machines or on-prem servers**
- Enable **real-time monitoring** of logs

## Cloudwatch Logs for EC2

- by default, no logs from your EC2 instance will go to CloudWatch
- you need to run a cloudwatch agent on EC2 to push the logs files you want
- ensure IAM permissions are correct
- cloudwatch log agent can be on-prem too

## Amazon EventBridge

- schedule: cron jobs
- event pattern: event rules to react to a service doing something
    - ex: Root user sign in event alert → SNS notification
- **schema registry**: model event schema
- archive events sent to an event bus
- c**an replay archived events**

## CloudTrail - Overview

- provide governance, compliance, and audit for your AWS acct
- CloudTrail is enabled by default
- Get history of events / API calls made w/i your AWS acct by:
    - console
    - SDK
    - etc
- a trail can be applied to all regions (default) or a single region
- **if API needs to be reviewed = CloudTrail**

## AWS X-Ray

- debugging in production, the good old way:
    - test locally
    - add log statements everywhere
- Log formats differ across apps and log analysis is hard
- debugging: one big monolith “easy”, dist. services “hard”
- no common views of your entire architecture
- enter… x-ray!
- visualize services and connections
- Advantages:
    - troubleshooting perf.
    - understand dependencies in a microservice architecture
    - pinpoint service issues

## Amazon CodeGuru

- ML-powered service for automated code reviews and app perf. recommendations
- provide 2 functionalities
    - CodeGuru Reviewer: automated code reviews for static code analysis
    - CodeGuru Profiler: visibility/recommendations about app perf. during runtime

## CodeGuru Reviewer

- identifiy critical issues, sercurity vuln. and hard-to-find bugs
- use ML and automated reasoning
- 

## CodeGuru Profiler

- help understand runtime behavior of your app
- features:
    - ID and remove code inefficiencies
    - improve app perf.
    - decrease compute costs
    - min. overhead on apps

## AWS health dashboard - service history

- show all regions, all services
- general info

## Your Account dashboard

- alerts and remediation guidance when events may impact you
- personalized view into the perf. and avail. of AWS services
- dashboard displays relevant and timely info with proactive notification to help plan scheduled activities
- can aggregate data from an entire AWS org
- global service
- show how AWS outages directly impact you & your AWS resources
- alert, remediation, proactive, scheduled activities

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de6d737a-13b0-428a-9952-e1d4fbc71b5b/Untitled.png)

## 

## VPC & Networking

VPC - virtual private cloud

- VPC is something for architect associate to know
- in this exam, should know
    - subets, internet gateways
    - sec groups, ACL
    - VPC endpoints
    - Site to Site VPN
- broad understanding only needed

## Ip addr in AWS

- IPv4
    - public IPv4 - can be used in internet
        - ec2 get new public IP every time you stop and start (default)
    - Private IP - only for private networks
        - fixed IP even start and stop for ec2
- **Elastic IP - allow attach fixed public IPv4 addr to EC2 instances**
    - note: has ongoing cost if not attached to EC2 instance or if the EC2 instance is stopped

- IPv6
    - every Ip is public

## VPC & subnets primer

- VPC
    - private network to deploy your resources
- subnet
    - allow you to partition your network inside your VPC
- public subnet
    - subnet that is accessible from internet
- private subnet
    - subnet that is not accessible from internet
- route tables
    - define access to internet and subnets

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de1712f4-dbee-4621-bdea-6bf7e233641b/Untitled.png)

## Internet Gateway & NAT Gateways

- Internet Gateways
    - **help our VPC instances connect w internet**
    - public subnets have route to internet gateway
    - **NAT Gateway & NAT instances allow your instances in ur private subnets to access the internet while remaining private**

## Network ACL & Security Groups

- NACL (Network ACL)
    - firewall controls traffic from and to subnet
    - can have ALLOW and DENY rules
    - are attached at subnet lvl
- Security Groups
    - a firewall controls traffic to and from an ENI / IC2 instance
    - can have only ALLOW rules
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/96ce819a-48b2-4d0d-92ff-9ae2d6ef58f9/Untitled.png)

## VPC Flow Logs

- capture info about IP traffic going into your interface:
    - VPC flow logs
    - subnet flow logs
    - elastic network interface flow logs
- help monitor & troubleshoot connecvity issues
    - subnet to internet
    - subnet to subnet etc.
- 

## VPC Peering

- connect two VPC, privately using AWS network
- make behave like in same network
- must NOT overlap CIDR
- VPC peering connection is not transitive

## VPC endpoints

- endpoints allow you to connect to AWS using private network instead
- gives enhanced security

## PrivateLink

- most secure & scalable way to expose a service to 1000s of VPCs
- does not require VPC peering
- requires a net. LB and ENI
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d7e6a662-f34c-46e4-86a9-a0b0dc6f670f/Untitled.png)

## Site 2 site VPN & direct connect

- Site to Site VPN
    - Connect an on-prem VPN to AWS
    - conn is auto encrypted
    - goes over public internet
    - on-prem: use **Customer Gateway**
    - AWS: use **Virtual Private Gateway**
- Direct Connect
    - est. physical conn btwn on-prem and AWS
    - goes over private network

## AWS Client VPN

- connect from pc using openvpn to ur private net in aws on-prem
- allow you to connect to your ec2 instances over private IP
- goes over public internet

## Transit Gateway

- for transitive peering btwn 1000s of VPCs and on-prem, hub and spoke
- one single gateway
- 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4dd33b48-8a8e-4e8a-ad76-52087b2cd2f4/Untitled.png)

## VPC Closing comments

- VPC: Virtual Private Cloud
- Subnet: tied to AZ, net partition of VPC
- Internet Gateway: at VPC lvl, provide internet access
- NAT Gateway: give internet access to private subnet
- NACL: Stateless, subnet rules for inbound and outbound
- Security Groups: stateful, operate at EC2 instance lvl or ENI
- VPC peering: connect 2 VPC w non overlapping IP ranges, non-transitive
- Elastic IP - fixed public IPv4, ongoing cost if not in-use
- VPC endpoints: provide private access to AWS services within VPC
- PrivateLink: private connect to a service in a 3rd party VPC
- VPC flow logs: network traffic logs
- Site 2 site VPN: connect btwn on-prem DC and AWS
- Client VPN: OpenVPN conn from your computer into your VPC
- Direct connect: direct private conn to AWS
- Transit Gateway: connect 1000s of VPC and on-prem together

## Security & Compliance

- AWS resp - Sec of the Cloud
    - protecting infra. that runs all the AWS services
    - managed services like s3, dynamoDB, RDS
- Customer resp. - Sec. in Cloud
    - EC2 insta. mgmt of guest OS, firewall, net config, IAM
    - encrypting app data
- Shared controls
    - Patch mgmt, config. mgmt, awareness & training
- 

## DDOS Attack Protection

- AWS Shield Std: protects against DDOS attack for your website and app, for all apps, for all cust at no additional costs
- AWS Shield Adv.: 24/7 premium DDos protection
- AWS WAF: filter specific req based on rules
- CloudFront and Route 53
    - avail protection using edge net
- be ready to scale - leverage AWS auto scaling

## AWS Shield

- Shield Std: free for every AWS customer, protect against SYN/UDP floods
- **Shield Adv**: if you need response team and more protection

## AWS WAF

- protect your web app form common web exploits
- l7 is HTTP
- Deploy App Load Balancer, API Gateway, CloudFront
- Define web ACL
    - rule can include IP addr., HTTP headers, HTTP body
    - protects from common attack - SQL injection and XSS
    - size constraints, geo-match
    - rate-based rules - for DDoS protection

## AWS Net Firewall

- protect entire Amazon VPC
- L3 to L7 protection
- Any direction, you can inspect
    - VPC to VPC traffic
    - outbound to internet
    - inbound from internet

## Pen testing on AWS Cloud

- AWS cust. are welcome carry out sec assessment or pen test against their AWS infra. **wo prior approval for 8 services**
- Prohibited activities
    - DNS zone walking via Route 53 hosted zones
    - DoS, DDos
    - port flooding
    - protocol flooding
    - request flooding
    - need approval from AWS security team

## Data at rest vs Data in transit

- at rest: data or archived on a device
    - on a physical instance somewhere
- in transit: data moving from 1 loc to another
    - transfer on network
- we want to encrypt data in both states
- leverage encryption keys

## AWS KMS

- key mgmt service = mgmt of keys on AWS
- encryption on AWS = KMS

## CloudHSM

- KSM ⇒ AWS manage software for enc
- CloudHSM ⇒ AWS provision enc hardware
- Dedicate security module
- you manage your keys not AWS

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80282769-a4ae-4c52-a2e0-878e42f394b0/Untitled.png)

## Type of cust. master keys: CMK

- Cust. mg CMK
    - create, mge, & used by cust. can enable or disable
- AWS mg CMK
    - create, mge, and used on cust. behalf by AWS
    - use by AWS services
- AWS owned CMK
    - collection of CMKs that AWS service owns and manage to use multiple accts
- CloudHSM Keys
    - Keys generate from own CloudHSM device

## AWS cert manager

- let you easy provision, manage, deploy SSL/TLS cert
- use in-flight enc. for websites
- support both public and private TLS certificate
- auto TLS cert renewal

## AWS Secrets Manager

- newer service, meant to storing secrets
- capability to force rotation of secrets every X days
- auto generation of secrets on rotation
- integration with Amazon RDS
- secrets are enc. using KMS
- For exam: if secret mgmt needed in RDS = Secret Manager

## AWS Artifact

- portal provide cust with on-demand access to AWS compliance doc and AWS agreements
- Artifacts reports - allow you to download AWS sec. and compliance doc from 3rd party
- artifact agreements- track status of AWS agreements for your account

## Amazon GuardDuty

- Int. threat discovery to protect AWS acct
- use ML, anomaly detection, 3rd party data
- **protect against cryptocurrency attack**

## Amazon Inspector

- auto sec assessment
- for ec2 instance
    - leverage AWS system manager agent
    - running OS against know vulns
- for container images push to Amazon ECR
    - assessment of container images as they are pushed
- for lambda functions
    - id software vulns in function code and package dependencies
    - assessment of func

What does inspector evaluate?

- **only for EC2 instances, container imgs & lambda funcs.**
- cont. scanning of infra. only when needed
- package vulns - db of CVE
- net reachability

## AWS Config

- help with auditing and recording compliance of your AWS resources
- help record configs and changes over time

## Amazon Macie

- fully managed data sec and data privacy uses ML and pattern matching to discover and protect your sensitive data in AWS
- id and alert you to sensitive data, such as PII

AWS Security Hub

- central security tool across several AWS accts and automate sec checks
- dashboard show current sec and compliance status
- first must enable AWS config to work

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01b4a34a-9e9e-4131-9434-1803d2bfe82f/Untitled.png)

## Amazon Detective

- when find sec. issues
- this service create deep analysis to get root cause of sec issues using ML
- auto collect and processes events

## AWS Abuse

- **report suspect AWS resources use for absuive and illegal purposes**

## Root user privileges

- root user = acct. owner
- complete access to all AWS services and resources
- **lock away root user access keys**
- Actions than can only be done by root user:
    - **change acct settings**
    - **close your AWS acct**
    - restore IAM user permissions
    - **change or cancel your AWS support plan**
    - **register as seller in reserved instance marketplace**

## IAM access analyzer

- find out which resources shared externally
    - s3 buckets
    - iam rules
    - kms keys
- Define Zone of Trust = AWS acct
- Access outside zone of trust ⇒ findings

# Account Mgmt, Billing & Support

## AWS Organization

- global service
- allow manage multiple AWS accts
- main acct is the master acct
- cost benefits
    - consolidated billing across all accts - single payment method
    - aggregated usage
- Pooling of Reserved EC2 instances for optimal savings
- API avail. to **automate AWS acct creation**
- Restrict acct privileges using Service Control Policies

Multi Acct Strats

- create accts per dept, per cost center, per dev test or prod, based on regulatory restrictions for resource isolation

OU examples - pick any

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/847a1e6d-f3be-4ead-91ae-b54e22cfff61/Untitled.png)

## Service Control Policies (SCP)

- whitelist or blacklist IAM actions
- applied at OU or acct lvl
- doesn’t apply to master acct.
- SCP applied to all users and roles of the acct., including root
- Must have explicit allow
- use case
    - restrict access to certain services

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f71468f-2098-4266-b0b3-2355ba4a1d96/Untitled.png)

## AWS Org. - Consolidated Billing

- when enabled, provides you with
    - combined usage - combine usage across all AWS accts in AWS org to **share volume pricing, reserved instances and savings plans discounts**
    - **one bill for all accts in org**

## AWS Control Tower

- easy way to set up and **govern a secure and compliant multi-acct. AWS env.**
- benefits
    - automate the set up of your env in few clicks
    - automate ongoing policy mgmt
    - detect policy violations and remediate them
- AWS control tower runs on top of AWS orgs
    - it auto set up AWS orgs to organize accts and implement SCPs

## AWS Resource access manager

- share AWS resources that you own with other AWS accts.
- share with any acct or within your org
- avoid resource duplication

## AWS Service Catalog

- user that are new to AWS may not be compliant with the rest of the org
- some users just want quick **self-service portal to launch authorized products by admins**

## Pricing Models of the Cloud

- 4 pricing models
    - pay as you go
    - save when you reserve
    - pay less by using more: volume based discounts
    - pay less as AWS grows

## Free services & free tier in AWS

- IAM
- VPC
- consolidated billing
- free but …pay for resources created:
    - elastic beanstalk
    - cloudformation
    - auto scaling groups

## Compute pricing - EC2

- only charged for what you use
- # of instances
- instance config.:
    - physical capacity
    - region
    - OS and software
    - instance type
    - instance size
- ELB running time and amount of data processed
- On-demand instances:
    - min of 60s
    - pay per sec or per hour
- Reserved instances
    - up to 75% discount compared to on-demand on hourly rate
- Spot instances
    - up to 90% discount compared to on-demand
    - risk of losing spot if someone else pays more
- Dedicated host
    - on-demand
    - reservation for 1 yr

## Lambda & ECS

- Lambda
    - pay per call
    - pay per duration
- ECS
    - EC2 launch type model: no additional fees, pay for AWS resources stored and created in your app
- Fargate
    - fargate launch type model: pay for vCPU and memory resources allocated to your apps in your containers

## Storage pricing - S3

- storage class: s3 std., s3 IA
- # and size of objs: price  can be tiered

## Storage pricing - EBS

- volume type
- storage volume in GB per month **provisioned**
- inbound=  free; outbound = pricing

## DB pricing - RDS

- per hr billing
- DB characteristics
- Purchase Type
- Backup Storage: No additional charge for backup storage up to 100% of your total db storage for a region
- outbound = paid; inbound = free

## Content Delivery - CloudFront

- pricing is different across different geographic regions
- aggregated for each edge loc, then applied to bill

## Networking costs in AWS per GB

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a981c1e-a766-4b56-9837-4f242fc6b6c0/Untitled.png)

## Savings Plan

- commit a certain $ amount per hour for 1 or 3 years
- easiest way to setup long-term commitments on AWS
- **EC2 savings plan**
    - commit to usage of individual instance families in a region
- Compute Savings plan
    - regardless of family, region, compute options
- ML savings plan

## AWS compute optimizer

- **reduce costs and improve perf.** by recommending optimal AWS resources for your workloads
- helps you choose optimal configs and right-size your workloads
- use ML to analyze your resources’ confgs and their **utilization CloudWatch metrics**
- lower cost by 25%

## Billing and Costing Tools

- estimating costs in cloud
    - pricing calculator
- Tracking costs in the cloud
    - billing dashboard
    - cost allocation tags
    - cost and usage reports
    - cost explorer
- Monitoring against costs plans
    - billing alarms
    - budgets

## AWS pricing calculator

- estimate cost for your solution architecture

## AWS billing dashboard

cost allocation tags

- use tag to track your AWS costs on detailed lvl
- AWS generated tags
    - automatically applied to resource you create
    - starts with prefix aws:
- User-defined tags
    - defined by user
    - starts with prefix user:

## Tagging and Resource Groups

- tags used for orgnizing resources
    - EC2: instances, imgs…
- free naming, common tags are: name, environment, Team
- Tags can be used to create **Resource Groups**
    - create, maintain, and view a collection of resources that share common tags
    - manage these tags using Tag Editor

## Cost and Usage Report

- diver deeper into AWS costs and usage
- most comprehensive set of AWS cost and usage data available
- lists AWS usage for each service category used by an acct and its IAM user in hourly

## Cost explorer

- visualize, understand, manage your AWS cost and usgae over time
- create custom reports to analyze cost and usage data
- Chooses an optimal savings plan
- **forecast usage up to 12 months** based on previous usage

## Billing Alarms in CloudWatch

- Billing mertic is stored in CloudWatch us-east-1
- billing are for overall worldwide AWS costs
- for actual costs, not for projected costs
- intended a simple alarm

## AWS budget

- **create alarm when budget is exceeded**
- up to 5 SNS notifications per budget

## AWS Cost anomaly detection

- **continuously monitor your cost and usage using ML to detect unusual spends**

## AWS Service Quotas

- notify when you’re close to service quote value threshold
- create cloudwatch alarms on service quotas console
- request a quota increase from AWS Service Quotas or shutdown resources before limit is reached

## Trusted Advisor

- no need to install anything - high level AWS account assessment
- analyze your AWS accts. and provides recommendation on 5 categories
    - Cost optimization
    - Performance
    - Security
    - Fault Tolerance
    - Service limits
- Support plans
    - 7 core checks
        - basic and developer support plan
            - s3 bucket permissions
            - sec groups
            - IAM Use
            - MFA on root acct
            - EBS public snapshots
            - RDS public snapshots
            - service limits
        - Full Checks
            - Business & Enterprise Support Plan
                - full checks available on 5 categories
                - ability to set CloudWatch alarms when reaching limits
                - programmatic access using AWS support API
                
    
    ## AWS Support Plans Pricing
    
    - Basic Support: free
        - customer service & communities
        - AWS Trusted Advisor
        - AWS personal health dashboard - personalized view of health of AWS services and alerts when your resources are impacted
    - AWS Developer Support Plan
        - Business hours email access to Cloud Support Associates
        - unlimited cases and 1 primary contact
        - Case Severity and response times
            - general guidance: < 24 hours
            - sys. impaired: < 12 hours
    - AWS Business Support Plan
        - Intended to be used if you have production workloads
        - trusted advisor - full set of checks + API Access
        - **24x7 phone, email, and chat access**
        - case response time
            - **prod system impaired: < 4 hours**
            - **prod sys down: < 1 hour**
    - AWS Enterprise on-ramp support plan
        - for production or business critical workloads
        - access to pool of **technical account managers**
        - concierge support team
        - infra. event management, well-architected & operations reviews
        - case response times
            - **business critical sys down: < 30 mins**
    - AWS Enterprise Support Plan
        - intended for mission critical workloads
        - all of business support plan +:
        - designated **technical account manager**
        - case response times
            - **business critical sys down: < 15 mins**
    
    # Machine Learning
    
    ## Amazon Rekognition
    
    - find obj, people, text, scenes in images and videos using ML
    - **facial analysis and facial search**
    
    ## Transcribe
    
    - auto convert speech to text
    - uses a deep learning process called auto speech recognition
    - **auto remove PII using redaction**
    
    ## Amazon Polly
    
    - turn text into lifelike speech using deep learning
    - allow to create app that talk
    
    ## Translate
    
    - natural and accurate language translation
    
    ## Lex & Connect
    
- Amazon Lex
    - Auto speech recognition to convert **speech to text and understand intentions**
    
    ## Amazon Connect
    
    - receive call, create contact flows, cloud-based **virtual call contact center**
    
    ## Comprehend
    
    - For NLP - Natural Language Processing
    - fully managed and serverless service
    - use ML to **find insights and relationships in text**
    
    ## SageMaker
    
    - fully managed service for dev to **build ML models**
    
    ## Forecast
    
    - fully managed service that uses **ML to deliver highly accurate forecasts**
    
    ## Kendra
    
    - **document search service** with ML

## Personalize

- ML service to build app with real-time personalized recommendations

## Textract

- **automatically extracts text**, handwriting, and data from any scanned documents using AI and ML
- extract from forms and tables
- read and process any type of doc

# Advanced Identity

## AWS Security token Service (STS)

- **temp, limited privileges credentials** to access resources

## Amazon Cognito

- **ID for your web and mobile app users - SSO**
- instead creating them an IAM user, you create a user in cognito

## What is MS AD?

- found on any windows server with AD domain services
- db of objs
- centralized security management, create acct, assign permissions

## AWS Directory Services

- MS AD = AWS Directory Services

## AWS IAM Identity Center

- **one login for all your AWS accts** in AWS orgs
- Identity providers
    - built-in identity store in IAM Identity center

## Other AWS Services

## WorkSpaces

- DaaS to provision windows or linux desktops
- eleiminate mgmt of on-prem VDI

<add more services here>

## AWS Architecting & Ecosystem

## Well Architected Framework - 6 pillars

1. operational excellence 
2. security 
3. reliability
4. performance efficiency
5. Cost optimization
6. Sustainability

## operational excellence

- run and monitor sys to deliver business value to continually improve support processes and procedures
- Design principles
    - perform ops as code
    - annotate documentation

## Security

- Design principles
    - implement strong identity foundation
    - enable traceability - logs
    - apply security at all layers
    - automate sec best practices

## Reliability

- ability of system to recover from infra or service disruptions
- Design principles
    - stop guessing capacity
    - test recovery procedures

## Performance Efficiency

- Design Principles
    - Democratize advanced technologies
    - go global in minutes

## Cost optimization

- ability to run systems to deliver business value at lowest price point
- Design principles
    - adopt consumption mode
    - measure overall efficiency

## AWS Well-Architected Tool

- AWS advice on how to design infra based on questions

## AWS Cloud Adoption Framework

- help build and execute comprehensive plan for digital transformation through innovation use of AWS
- AWS CAF Groups: **Business, People, Governance, Platform, Security, and Operations**
    - Business = ensure cloud investment help business outcomes
    - People = bridge between tech and business to make culture of cont. growth
    - Governance = orchestrate cloud initiatives while max org benefits and min transformation risks
    - Platform = help build enterprise-grade hybrid cloud platform
    - Security = help achieve CIA
    - Operations = ensure cloud services at lvl that meets business needs

## AWS CAF - Transformation Domains

- technology - using cloud to migrate and modernize legacy infrastructure, apps, data, and analytics platform
- Process - digitizing, automating, and optimizing your business operations
- Organization - reimaging your operating model
- Product - reimaging your business model by creating new value propositions and revenue models

## AWS Right sizing

- Ec2 the most powerful instance isn’t always the best choice bc cloud is elastic
- **this matches instance types and size to workload performance and capacity reqs. at lowest possible cost**

## AWS Knowledge Center

- common questions and answers page

## AWS IQ

- quickly find professional help for AWS projects
- engage and pay 3rd party expert for project work

## AWS Managed Services

- provide infra and app support on AWS
- **AMD offers a team of AWS experts** who manage and operate infra
- 24/365
