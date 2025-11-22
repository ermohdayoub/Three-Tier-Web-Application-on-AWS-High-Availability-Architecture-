# Three-Tier-Web-Application-on-AWS-High-Availability-Architecture-

This project demonstrates the design and deployment of a secure, scalable, and highly available 3-Tier Web Application on Amazon Web Services (AWS).
It uses a fully customized VPC with public and private subnets, EC2 instances across multiple Availability Zones, an Application Load Balancer, RDS MySQL, phpMyAdmin, and secure networking components such as NAT Gateway, Route Tables, Security Groups, and a Jump/Bastion Server.

##Screenshot of EC2 Instances 
<img width="1919" height="881" alt="Screenshot 2025-10-03 202704" src="https://github.com/user-attachments/assets/7d7c95a3-4258-4af0-9c36-d693d9f3906d" />

##Screenshot of RDS Dashboard
<img width="1919" height="877" alt="Screenshot 2025-10-03 202926" src="https://github.com/user-attachments/assets/909e7c00-d94c-43f3-92db-db3a9365af92" />

##Screenshot of Load balancer
<img width="1919" height="888" alt="Screenshot 2025-10-03 202811" src="https://github.com/user-attachments/assets/ac61ce17-9eb7-444c-9ace-2bcc88ab5cc8" />

##Screenshot of Jump Server SSH
<img width="1919" height="877" alt="Screenshot 2025-10-03 202638" src="https://github.com/user-attachments/assets/98a5d33f-29bd-49a2-9f38-aa7db51c3776" />

##Screenshot of Route Tables
<img width="1919" height="866" alt="Screenshot 2025-10-03 202446" src="https://github.com/user-attachments/assets/b8f45c69-7d8b-4038-acae-68f0f01934f3" />

##Screenshot of VPC Resource Map
<img width="1919" height="881" alt="Screenshot 2025-10-03 202300" src="https://github.com/user-attachments/assets/dcc461e8-9e1b-41cf-bdc5-43de723252e2" />

##Screenshot of PHP Server Outputs
<img width="1913" height="1015" alt="Screenshot 2025-09-30 015345" src="https://github.com/user-attachments/assets/1b997fd3-0f70-4349-888e-ea9a49a6df57" />
<img width="1919" height="1019" alt="Screenshot 2025-09-30 015337" src="https://github.com/user-attachments/assets/27db4076-9960-483c-9044-cf2323b474bd" />

##Screenshot of phpMyAdmin
<img width="1919" height="1012" alt="Screenshot 2025-09-30 015815" src="https://github.com/user-attachments/assets/bf0a80fb-8062-4819-8eab-20f6418b3cb4" />
<img width="1913" height="1017" alt="Screenshot 2025-10-03 202951" src="https://github.com/user-attachments/assets/099cbed7-5f36-4c90-a987-ef7ee378c55e" />

This architecture follows AWS best practices for fault tolerance, high availability, and network isolation.
Architecture Overview:
 Web Tier (Public Subnets)
 - Accessible via the internet
 - Hosts the Application Load Balancer (ALB)
 - Receives all user traffic

 Application Tier (Private Subnets)
 - Contains two EC2 App Servers
 - Hosts PHP application and phpMyAdmin
 - Not accessible from the internet
 - Accessed only via ALB or Jump Server

 Database Tier (Private Subnets)
 - Amazon RDS MySQL instance
 - Completely private
 - Accessible only from App Tier

 AWS Services Used
 - Networking
 - Amazon VPC (20.0.0.0/20)
 - 6 Subnets across 2 Availability Zones
 - Internet Gateway (IGW)
 - NAT Gateway
 - Route Tables (Web, App, DB)
 - Security Groups (Web, App, DB, Jump server)

Compute
 - EC2 (Amazon Linux 2023)
 - App Server 1
 - App Server 2
 - Jump/Bastion Server

Load Balancing
 - Application Load Balancer (ALB)
 - Target Group with both App Servers
 - Health checks enabled

Database
 - Amazon RDS MySQL
 - Integrated with phpMyAdmin for DB management

Others
 - PHP & Apache Web Server
 - phpMyAdmin setup
 - SSH access via Jump Server

 VPC & Subnet Structure
Availability Zone: ap-south-1a
 - web-pub-sub1 — Public
 - app-pvt-sub1 — Private
 - db-pvt-sub1 — Private

Availability Zone: ap-south-1b
 - web-pub-sub2 — Public
 - app-pvt-sub2 — Private
 - db-pvt-sub2 — Private
VPC CIDR: 20.0.0.0/20

 Route Table Configuration
route-web
 - Internet Gateway route → Public Subnets

route-app
 - NAT Gateway route → Private App Subnets

route-db
 - Local-only routes → Private DB Subnets

 Application Load Balancer Setup
 - Listener: HTTP:80
 - Target Group: app-tg

Registered Targets:
 - app-server-1
 - app-server-2
- Health checks: ✔ Healthy

When accessing ALB DNS name:
 - One request returns → “PHP server 1”
 - Next request returns → “PHP server 2”

This confirms:
 - Load Balancing
 - Auto failover

Multi-AZ High Availability

 RDS & phpMyAdmin Integration
RDS MySQL
 - Engine: MySQL 8.x
 - AZ: ap-south-1a
 - Deployed in private subnets
 - No public accessControlled through Security Groups

phpMyAdmin
 - Installed on App Servers
 - Connects securely to RDS
 - Accessible through ALB URL
 - Verified with phpMyAdmin login screen

 Jump/Bastion Server
Jump server is placed in a public subnet to enable secure SSH access to:
 - app-server-1
 - app-server-2
 - Commands executed through jump server included:
 - Installing phpMyAdmin
 - Updating Apache/PHP
 - Configuring RDS credentials
 - File modifications (mv config.sample.inc.php config.inc.php)

 How the Application Works
1. User → ALB DNS → Public Subnet
2. ALB → Routes request to App Server 1 or 2
3. App Servers → Process PHP Application
4. App Servers → Connect to RDS
5. Response → Back to ALB → User

Skills Demonstrated
 - VPC Design & Subnetting
 - EC2 Deployment & Configuration
 - Load Balancer Setup
 - NAT & IGW configuration
 - Linux Administration
 - RDS Database Management
 - phpMyAdmin Deployment
 - Route Tables & Security Groups
 - Multi-AZ Application Architecture
 - Real-world 3-tier cloud deployment

👨‍💻 Author
Mohd Ayoub
AWS & DevOps Engineer
LinkedIn: (https://www.linkedin.com/in/ermohdayoub)

⭐ If you like this project
Please give the repository a star ⭐ — it really helps!
