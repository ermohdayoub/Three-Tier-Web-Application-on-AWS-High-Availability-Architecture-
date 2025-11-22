# Three-Tier-Web-Application-on-AWS-High-Availability-Architecture-

This project demonstrates the design and deployment of a secure, scalable, and highly available 3-Tier Web Application on Amazon Web Services (AWS).
It uses a fully customized VPC with public and private subnets, EC2 instances across multiple Availability Zones, an Application Load Balancer, RDS MySQL, phpMyAdmin, and secure networking components such as NAT Gateway, Route Tables, Security Groups, and a Jump/Bastion Server.

This architecture follows AWS best practices for fault tolerance, high availability, and network isolation.
Architecture Overview
✔ Web Tier (Public Subnets)

Accessible via the internet

Hosts the Application Load Balancer (ALB)

Receives all user traffic

✔ Application Tier (Private Subnets)

Contains two EC2 App Servers

Hosts PHP application and phpMyAdmin

Not accessible from the internet

Accessed only via ALB or Jump Server

✔ Database Tier (Private Subnets)

Amazon RDS MySQL instance

Completely private

Accessible only from App Tier

🏗️ AWS Services Used
Networking

Amazon VPC (20.0.0.0/20)

6 Subnets across 2 Availability Zones

Internet Gateway (IGW)

NAT Gateway

Route Tables (Web, App, DB)

Security Groups (Web, App, DB, Jump server)

Compute

EC2 (Amazon Linux 2023)

App Server 1

App Server 2

Jump/Bastion Server

Load Balancing

Application Load Balancer (ALB)

Target Group with both App Servers

Health checks enabled

Database

Amazon RDS MySQL

Integrated with phpMyAdmin for DB management

Others

PHP & Apache Web Server

phpMyAdmin setup

SSH access via Jump Server

🌐 VPC & Subnet Structure

From your actual setup and screenshots:

Availability Zone: ap-south-1a

web-pub-sub1 — Public

app-pvt-sub1 — Private

db-pvt-sub1 — Private

Availability Zone: ap-south-1b

web-pub-sub2 — Public

app-pvt-sub2 — Private

db-pvt-sub2 — Private

VPC CIDR: 20.0.0.0/20

🔐 Route Table Configuration
route-web

Internet Gateway route → Public Subnets

route-app

NAT Gateway route → Private App Subnets

route-db

Local-only routes → Private DB Subnets

⚙️ Application Load Balancer Setup

Listener: HTTP:80

Target Group: app-tg

Registered Targets:

app-server-1

app-server-2

Health checks: ✔ Healthy

When accessing ALB DNS name:

One request returns → “PHP server 1”

Next request returns → “PHP server 2”

This confirms:

Load Balancing

Auto failover

Multi-AZ High Availability

🗄️ RDS & phpMyAdmin Integration
RDS MySQL

Engine: MySQL 8.x

AZ: ap-south-1a

Deployed in private subnets

No public access

Controlled through Security Groups

phpMyAdmin

Installed on App Servers

Connects securely to RDS

Accessible through ALB URL

Verified with phpMyAdmin login screen

🔧 Jump/Bastion Server

Jump server is placed in a public subnet to enable secure SSH access to:

app-server-1

app-server-2

Commands executed through jump server included:

Installing phpMyAdmin

Updating Apache/PHP

Configuring RDS credentials

File modifications (mv config.sample.inc.php config.inc.php)

🧩 How the Application Works

User → ALB DNS → Public Subnet

ALB → Routes request to App Server 1 or 2

App Servers → Process PHP Application

App Servers → Connect to RDS

Response → Back to ALB → User
