# Solution Architect Associate - Syllabus


# Day 1 

## Elastic Compute Cloud (EC2) 

### Regions and Availability Zones

### Instance Types

### CloudWatch

### Elastic Block Store (EBS)

#### Volumes

##### Encryption

#### Snapshots

## Virtual Private Cloud (VPC) 

### VPC 

### CIDR (Classless Internet Domain Routing) - IP Address Ranges

### Subnets

### Route Tables

### Subnets Private vs Public 

### Integret Gateway

### NAT Gateway

### Network ACLs and Security Groups (firewalls)

## Identity and Access Management (IAM)

### Users & Groups

### IAM Policies

### IAM Roles

### Shared Responsibility Model

## EC2 - Scaling and Reliability 

### Auto Scaling Groups (ASG)

### Launch Template - like a blueprint

### Elastic Load Balancer (ELB)

## CloudTrail (Who dun it?)



# Day 2 

## S3

### "Super Powers" and features

### A place to put our To Do App Build

#### CloudShell and AWS CLI

## Relational Database Service

### Multi-AZ Instace vs Cluster  

### Encryption, Backups, Read Replicas

### Aurora vs other types

## DynamoDB 

### Basic features

### Database Table for To Do App

## Create an Instance Profile / Role / Policy for EC2
    SSMManagedInstanceCore
    S3ReadOnly 
    DynamoDBFull
    
## Install "To Do" via EC2 User Data 



## Simple Notification Service (SNS)

### Topics & Subscriptions

### Topic - for Notifications when a new Task is added

## Lambda

### Serverless Compute - FaaS

### A Lambda to export To Do Items into a CSV (and put into S3)

## Simple Queue Service (SQS)

### Decoupling using Queues

### Dropping a queue item into SQS queue -> Lambda -> Topic -> Notification when Export is done


# Day 3 

## CloudFormation (Infrastructure as Code)

## Elastic Container Service (ECS)

## CloudFront

## AWS Certified Solutions Architect - Associate

### Exams Tips and Tricks


