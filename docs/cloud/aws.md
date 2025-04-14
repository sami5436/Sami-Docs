# AWS

## Overview
AWS Services and Approach to Multi Tier Architecture 

### Topics Covered
- Compute: EC2, Lambda, Fargate, Auto Scaling
- Networking & Security: VPC, Subnets, NACLs, Security Groups, Route Tables
- Storage: S3, EFS, EBS
- Identity & Access: IAM, Cognito
- Monitoring & Logging: CloudWatch, CloudTrail
- API & Integration: API Gateway, SQS, SNS
- Databases: RDS, Redshift

## Full Breakdown


On 04/12/2025, I had the opportunity to attend my very first Cloudathon that introduced me to AWS. In preparation, I spent time learning fundamental AWS concepts such as identity management, compute, storage, and networking.

During the Cloudathon, I got hands-on experience working with real-world scenarios. I learned how to think critically about designing scalable and fault-tolerant architectures, and how various AWS services can be integrated to solve business problems.

We were given a problem statement that involved a company valued at over $10 million, operating in e-commerce, AdTech, and SaaS products had an on-prem architecture with a list of pain points. Our task was to migrate it to a cloud architecture.

Diving into it, I was confused on how to even begin. I decided to search up the most frequently used AWS services and begin from there. Here it is what I learned:

**Networking & Security**:
| Service | Icon | Description + Example |
|---------|-------|------------------------|
| VPC | <img src="images/aws/vpc.png" width="75"/> | A **Virtual Private Cloud** is your own logically isolated network in AWS. You control subnets, IP ranges, route tables, gateways, and firewall rules. <br>**Example:** Set up a VPC with private subnets for databases and public subnets for web servers to simulate a traditional data center setup. |
| Subnets | <img src="images/aws/subnet.png" width="75"/> | Subnets divide your VPC into smaller segments. Public subnets connect to the internet; private subnets do not. <br>**Example:** Place your ALB in a public subnet and your EC2 backend in a private subnet. |
| Multi-AZ | <img src="images/aws/multiaz.png" width="75"/> | Multi-AZ means deploying instances in different physical data centers (Availability Zones) to increase fault tolerance. <br>**Example:** Host your app in 2 AZs so it stays online even if one fails. |
| Internet Gateway | <img src="images/aws/igw.png" width="75"/> | An IGW connects public subnets to the internet. Without it, resources in your VPC cannot send/receive internet traffic. <br>**Example:** Your web server needs this to be accessible from users’ browsers. |
| NAT Gateway | <img src="images/aws/natgateway.png" width="75"/> | A NAT Gateway lets private subnet resources reach the internet (for updates, API calls), but prevents inbound access. <br>**Example:** An EC2 in a private subnet installs security patches without exposing itself. |
| Security Groups | <img src="images/aws/securitygroup.png" width="75"/> | Acts as a virtual firewall at the EC2 level. It is stateful and controls what traffic is allowed in or out of a specific resource. <br>**Example:** Allow only ports 22 and 443 for SSH and HTTPS on your Linux EC2. |
| Network ACLs | <img src="images/aws/nacl.png" width="75"/> | Optional stateless firewall rules applied at the subnet level. You can use it for deny rules or IP blocking. <br>**Example:** Block an IP range that's scanning your subnet using an inbound NACL rule. |
| Route Tables | <img src="images/aws/route-table.png" width="75"/> | Define how traffic flows within your VPC. Route public traffic to the IGW and internal traffic across subnets. <br>**Example:** Route app-tier traffic to database-tier using private IPs only. |

**Compute**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| EC2 | <img src="images/aws/ec2.png" width="75"/> | Elastic Compute Cloud gives you full control over virtual machines in the cloud. You choose OS, instance type, and storage. <br>**Example:** Run a Python Flask server on an EC2 Linux instance with an EBS volume. |
| Lambda | <img src="images/aws/lambda.png" width="75"/> | A serverless function that runs code without provisioning servers. It executes only when triggered, saving cost. <br>**Example:** Automatically resize images uploaded to S3 without managing any server. |
| Fargate | <img src="images/aws/fargate.png" width="75"/> | Serverless compute engine for running containers. You don’t manage EC2 or clusters. Works with ECS or EKS. <br>**Example:** Deploy a containerized Flask app with zero server management. |
| Auto Scaling | <img src="images/aws/autoscaling.png" width="75"/> | Automatically increases or decreases EC2 instances based on demand, health checks, or schedules. <br>**Example:** During high traffic hours, scale up EC2s behind a load balancer; scale down at night. |

**Storage**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| S3 | <img src="images/aws/s3.svg" width="75"/> | Simple Storage Service offers highly scalable object storage for files, backups, and static websites. <br>**Example:** Host a React app’s static files and images in a public S3 bucket. |
| EFS | <img src="images/aws/efs.svg" width="75"/> | Elastic File System is a shared POSIX-compliant file system for use with Linux EC2 instances. <br>**Example:** Mount a shared file directory across a fleet of EC2s running the same app. |
| EBS | <img src="images/aws/ebs.svg" width="75"/> | Elastic Block Store provides raw block-level storage that you can attach to EC2 like a hard disk. <br>**Example:** Store a database on a persistent EBS volume attached to your EC2. |


**Networking & Content Delivery**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| ALB | <img src="images/aws/alb.png" width="75"/> | Application Load Balancer routes HTTP(S) traffic to targets like EC2, Lambda, or containers. Supports path-based and host-based routing. <br>**Example:** Route `/api` traffic to EC2 and `/auth` traffic to Lambda. |
| CloudFront | <img src="images/aws/cloudfront.png" width="75"/> | Content Delivery Network that caches static and dynamic content in edge locations globally. <br>**Example:** Deliver a website’s media and assets faster to international users. |
| Route 53 | <img src="images/aws/route53.png" width="75"/> | DNS service that routes traffic globally. Supports domain registration, health checks, and failover. <br>**Example:** Register `example.com` and route it to your ALB with latency-based routing. |


**Identity & Access**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| Cognito | <img src="images/aws/cognito.png" width="75"/> | User identity management service with login/signup, OAuth, and MFA. Integrates with mobile/web apps. <br>**Example:** Add Google login and user pools to a React app with Cognito. |
| IAM | <img src="images/aws/iam.webp" width="75"/> | Identity and Access Management lets you define users, roles, groups, and policies to control access. <br>**Example:** Create a role that lets EC2 access only specific S3 buckets. |


**Databases**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| RDS | <img src="images/aws/rds.png" width="75"/> | Managed relational database service for MySQL, PostgreSQL, and more. Includes backups, patching, and Multi-AZ support. <br>**Example:** Deploy a PostgreSQL DB for your web app with auto failover enabled. |
| Redshift | <img src="images/aws/redshift.png" width="75"/> | Petabyte-scale data warehouse built for analytics and OLAP queries. Optimized for reporting. <br>**Example:** Run complex joins on billions of records from event logs or sales data. |


**Monitoring & Logging**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| CloudWatch | <img src="images/aws/cloudwatch.png" width="75"/> | Monitors resource usage, collects logs, creates dashboards, and sends alerts. <br>**Example:** Set up an alarm to notify when EC2 CPU > 80% for 5 minutes. |
| CloudTrail | <img src="images/aws/cloudtrail.png" width="75"/> | Records every action taken through AWS Console, CLI, or SDK for auditing and compliance. <br>**Example:** See who deleted an S3 bucket by reviewing CloudTrail logs. |


**API & Integration**:

| Service | Icon | Description + Example |
|---------|-------|------------------------|
| API Gateway | <img src="images/aws/apigateway.jpg" width="75"/> | Creates REST and WebSocket APIs. Easily connect frontend to Lambda, EC2, or backend services. <br>**Example:** Expose a Lambda-based backend via secure API endpoints. |
| SQS | <img src="images/aws/sqs.webp" width="75"/> | Queueing system for decoupling microservices. Ensures reliable message delivery. <br>**Example:** Handle 10,000+ orders per minute without crashing the backend. |
| SNS | <img src="images/aws/sns.webp" width="75"/> | Pub/Sub notification system that pushes messages to email, SMS, Lambda, or other endpoints. <br>**Example:** Send an alert email when your database instance restarts. |