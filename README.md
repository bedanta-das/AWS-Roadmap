# :cloud: AWS DevOps Roadmap – With Real-World Notes (2026)

<p align="center">
  <img src="Icons/AWS.png" width="30%" />
</p>

DevOps is a set of practices that combines development and operations to deliver software faster, more reliably, and with fewer failures.
Earlier, developers wrote code and handed it to operations. If something broke, they blamed each other. DevOps removes this gap by automating build, test, deployment, and monitoring.

Use this repo as your learning guide, revision notes, and interview prep.

## Prerequisites (Before Deep Diving into AWS)
You’ll understand this roadmap better if you already know:
* Basic Linux commands
  i. Files & permissions - ls, cd, cp, mv, rm, chmod, chown
  ii. Processes - ps, top, kill
  iii. Text Processing - grep, awk, sed
  iv. Networking basics - curl, netstat

## :cloud: AWS Fundamentals
AWS Fundamentals are your base layer.
This is where you understand how AWS is structured and how everything connects.

Key ideas you should be clear about:
Regions & Availability Zones: where your resources actually live physically.
Global services vs regional services: e.g., IAM is global, EC2 is regional.
Shared Responsibility Model: what AWS manages vs what you must secure and manage.
Free Tier: what you can use safely without getting a surprise bill (with limits).

In the real world, this understanding helps you make decisions like:
choosing the right region for latency and compliance
designing highly available systems using multiple AZs
knowing where data is stored and what happens when a region fails
Once this is clear, every other service feels less random and more logical.

## :cloud: DevOps lifecycle (Code → Production)

<p align="center">
  <img src="Icons/devops.jpg" width="60%" />
</p>

The DevOps lifecycle includes:
* Code – Developers write code and push to Git
* Build – CI tool builds the application
* Test – Automated tests run
* Package – App is containerized using Docker
* Deploy – Kubernetes deploys containers
* Monitor – Prometheus and Grafana monitor health

Real-World Example:
If I update a login feature:
* I push code to GitHub
* GitHub Actions builds Docker image
* Kubernetes rolls out the new version
* Grafana shows CPU and error metrics

## 1. IAM – Identity and Access Management

<img src="iam.png" width="400">

IAM controls who can do what in your AWS account.

It’s the core of security in AWS:
* Users, roles, groups, and policies define access.
* Access is controlled by JSON policies that allow or deny actions on resources.
* Roles are used heavily by EC2, Lambda, ECS, CI/CD, etc.

Real-world usage:
* Giving developers controlled access to specific services (like S3, EC2, ECR).
* Creating roles for EC2/Lambda so they can access S3 or DynamoDB securely.
* Enforcing least privilege so no one has more permissions than they actually need.
* Setting up MFA and secure access for production accounts.

As a DevOps engineer, you will:
* create and debug IAM roles and policies
* attach roles to EC2, ECS tasks, EKS, Lambda, and CI/CD tools
* fix “AccessDenied” issues all the time
* ensure production access is locked down
If IAM is weak, everything else is at risk.

## 2. EC2 – Elastic Compute Cloud

<img src="ec2.png" width="400">

EC2 is where you get virtual servers in the cloud.

Think of EC2 as:
* “I need a Linux/Windows machine with X CPU, Y RAM and Z disk.”
* You can SSH into it, install apps, run services, and configure it like a normal server.

Real-world use cases:
* Running backend services, APIs, cron jobs, batch processing.
* Hosting legacy apps that are not containerized or serverless.
* Jump/bastion hosts for admin access into private networks.

As a DevOps engineer, you will:
* launch and configure EC2 instances inside VPCs.
* manage security groups, key pairs, and roles.
* automate deployments to EC2 using tools like CodeDeploy, Ansible, or CI/CD pipelines.
* set up Auto Scaling Groups for high availability and scaling.
* monitor and troubleshoot CPU, memory, disk, and app performance.
If you understand EC2 deeply, a huge part of AWS compute becomes easier.

## 3. VPC – Virtual Private Cloud
VPC is your own private network inside AWS.

It’s where you design:
* how your resources are connected
* which are public-facing
* which stay private and locked down

Core pieces inside a VPC:
* Subnets (public vs private)
* Route tables
* Internet Gateway and NAT Gateway
* Security Groups and Network ACLs

Real-world use cases:
* Isolating environments like dev, staging, and prod.
* Placing databases in private subnets and only exposing apps via load balancers.
* Connecting on-prem data centers to AWS using VPN or Direct Connect.
* Controlling which services can call each other.

As a DevOps engineer, you will:
* design network layouts for new workloads.
* place EC2, RDS, EKS, ECS correctly within the VPC.
* open and close ports using security groups.
* debug connectivity issues like “can’t reach the database” or “service timeout.”
* set up NAT for private resources that need internet updates but shouldn’t be exposed.
Without VPC, AWS will always feel confusing. Once this clicks, everything starts to feel structured.

## 4. AWS Security Best Practices
Security is not one service, it’s a mindset plus a set of tools.

Key areas to think about:
* Access control (IAM, roles, MFA, SSO)
* Data protection (encryption at rest and in transit)
* Network security (VPC, security groups, NACLs)
* Monitoring & logging (CloudTrail, CloudWatch, Config)
* Secrets management (Secrets Manager, Parameter Store)

Real-world use:
* Enforcing MFA and role-based access in production accounts.
* Encrypting S3, RDS, EBS volumes.
* Using security scanners, guardrails, and policies.
* Doing regular security reviews and checking CloudTrail logs.

As DevOps, you sit in the middle of:
* developers who want to move fast
* security teams who want things locked down
You help build systems that are both safe and practical.

## 5. Route 53 – DNS & Traffic Routing
Route 53 is AWS’s DNS service.

What it helps with:
* Mapping your domain (example.com) to AWS services like EC2, ALB, CloudFront, or S3.
* Health checks for failover.
* Advanced routing (weighted, latency-based, geo-based).

Real-world usage:
* Pointing app.yourdomain.com to your load balancer or CloudFront.
* Blue/green or canary traffic shifting using weighted records.
* Multi-region failover setups.

As a DevOps engineer, you will:
* manage records for application domains.
* connect your DNS provider (or move to Route 53).
* handle cutovers during migrations and deployments.
* debug “site not loading” issues related to DNS.
DNS issues can look like magic. Knowing Route 53 helps you de-mystify them.

## 6. S3 – Simple Storage Service
S3 is object storage for almost anything.

Real-world data stored in S3:
* logs, backups, images, videos
* static websites
* deployment artifacts
* data lakes for analytics

Why it’s important:
* It’s durable (designed for 11 9s).
* It’s cheap for the amount of data it can hold.
* It integrates with almost everything in AWS.

As a DevOps engineer, you will:
* store build artifacts from CI/CD pipelines.
* configure S3 buckets for logging (ALB/CloudFront logs).
* host static sites using S3 + CloudFront.
* manage bucket policies, encryption, and lifecycle rules for cost savings.
* set up cross-account or cross-region access when needed.
S3 will appear in almost every project you touch.

## 7. AWS CLI & Automation
The AWS CLI lets you talk to AWS from the terminal.

Instead of clicking in the console, you can:
* script tasks
* automate things
* integrate AWS with your tooling and workflows

Real-world use:
* writing shell scripts that create, update, or destroy resources.
* pulling logs, metrics, and data quickly.
* running deployments and maintenance tasks across multiple accounts/regions.

As a DevOps engineer, you will:
* configure multiple profiles for different environments.
* use the CLI in CI/CD pipelines.
* mix the CLI with Bash/Python scripts for one-off automation.
* quickly debug resources when console is painful to use.
This is a must-have skill to feel “comfortable” with AWS as an engineer, not just a console user.

## 8. CloudFormation – Infrastructure as Code (IaC)
CloudFormation lets you define your infrastructure as YAML/JSON templates.

You describe:
* “I want a VPC, 2 subnets, 3 EC2 instances, an RDS, and an ALB” in a file, and CloudFormation creates it for you.

Real-world usage:
* repeatable environments (dev, test, prod) with the same config.
* version control of infrastructure.
* safer changes using change sets and rollbacks.

As a DevOps engineer, you will:
* write and maintain CloudFormation templates or modules.
* deploy stacks from CI/CD pipelines.
* manage parameters, outputs, nested stacks.
* debug failed stack creations and updates.
CloudFormation is powerful but can feel verbose. Understanding it helps you unlock more advanced IaC flows.

## 9. Terraform is another IaC tool, but cloud-agnostic.

You define your infrastructure in .tf files and Terraform:
* plans what will change
* applies those changes
* keeps track in a state file

Real-world usage:
* managing multi-cloud or hybrid-cloud infra.
* building reusable modules for common patterns.
* using remote state (e.g., S3 backend) for team collaboration.

As a DevOps engineer, you will:
* create Terraform modules for VPCs, ECS/EKS clusters, databases, etc.
* manage state files carefully (especially in teams).
* integrate Terraform with CI/CD to safely roll out infra changes.
* review Terraform plans during pull requests.
Terraform is extremely valuable in modern DevOps teams and is often a key interview topic.

## 10. AWS Developer Tools – CodeCommit, CodeBuild, CodeDeploy
These are AWS’s own CI/CD building blocks.
* CodeCommit: Git repo (like GitHub, but on AWS).
* CodeBuild: build server to compile, test, and package code.
* CodeDeploy: handles deployments to EC2, ECS, or Lambda.

Real-world usage:
* fully AWS-native CI/CD pipelines.
* deployments that integrate tightly with IAM and VPCs.
* on-prem replacement for legacy Jenkins setups in some teams.

As a DevOps engineer, you will:
* write buildspec.yml for CodeBuild.
* configure CodeDeploy apps & deployment groups.
* manage deployment strategies like rolling, blue/green.
* plug these services into CodePipeline.
Even if your company uses GitHub Actions/GitLab etc., knowing these tools helps you understand AWS-native CI/CD.

## 11. CodePipeline – CI/CD Automation
CodePipeline ties everything together.

You define a pipeline like:
* Source (GitHub/CodeCommit)
* Build (CodeBuild)
* Test (optional)
* Deploy (CodeDeploy, ECS, Lambda, CloudFormation, etc.)

Real-world usage:
* automated deployments on every push or tag.
* multi-environment pipelines (dev → test → prod).
* manual approvals before production deployments.

As a DevOps engineer, you will:
* build and maintain CodePipelines.
* connect stages with artifacts.
* handle rollback strategies.
* integrate security checks, tests, and notifications.
This is where your “DevOps” part really shows: shipping code reliably and repeatedly.

## 12. CloudWatch – Monitoring & Logging
CloudWatch is your eyes inside AWS.

It handles:
* metrics (CPU, memory via agents, latency, etc.)
* logs (application logs, system logs, Lambda logs, ALB logs)
* alarms (trigger alerts when things go wrong)
* simple dashboards.

Real-world usage:
* alerting when CPU/RAM spikes or error rates increase.
* centralizing logs for debugging.
* creating dashboards for SRE/DevOps teams and stakeholders.
* triggering actions (like Lambda) when certain patterns are seen.

As a DevOps engineer, you will:
* forward logs to CloudWatch from EC2, ECS, Lambda, etc.
* create alarms for critical metrics (e.g., 5xx errors, queue depth).
* set up dashboards for observability.
* integrate CloudWatch alarms with Slack/Email/PagerDuty.
You can’t operate production systems blindly. CloudWatch is the base of observability in AWS.

## 13. Lambda – Serverless Functions
Lambda lets you run code without managing servers.

You just:
* upload your code (or container)
* define how it’s triggered
* pay only for the execution time

Real-world usage:
* processing S3 uploads (e.g., resize image, process CSV).
* cron jobs (scheduled tasks).
* lightweight APIs (with API Gateway).
* glue between services (e.g., EventBridge → Lambda → DB).

As a DevOps engineer, you will:
* set up Lambda permissions (IAM roles).
* configure triggers (S3, EventBridge, API Gateway, SNS, SQS).
* manage environment variables and secrets.
* monitor Lambda performance, cold starts, and errors.
Lambda is heavily used in modern event-driven and microservice architectures.

## 14. CloudFront – Content Delivery Network
CloudFront speeds up content delivery across the world.

It:
* caches your content (S3 files, website assets, APIs) at edge locations.
* helps reduce latency for global users.
* can add security with features like WAF and signed URLs.

Real-world usage:
* fronting static websites (S3 + CloudFront).
* protecting and accelerating APIs.
* serving media content (images, videos) efficiently.

As a DevOps engineer, you will:
* configure CloudFront distributions.
* connect CloudFront with S3/ALB/APIs.
* set cache behaviors and invalidations.
* manage SSL certificates via ACM.
CloudFront is essential if you care about performance for users in multiple regions.

## 15. ECR – Elastic Container Registry
ECR is a private Docker image registry on AWS.

You push images here, then run them on ECS or EKS.

Real-world usage:
* storing application images for microservices.
* versioning images for rollbacks and deployments.
* integrating with CI/CD to push new images after builds.

As a DevOps engineer, you will:
* create and manage ECR repositories.
* set up IAM-based authentication for CI/CD and clusters.
* scan images for vulnerabilities (if enabled).
* clean up old images to save cost.
ECR is a core part of any container-based AWS setup.

## 16. ECS – Elastic Container Service
ECS is AWS’s managed container orchestrator.

You define:
* Task definitions (what containers to run)
* Services (how many tasks, scaling, restarts)
* Launch type (EC2 or Fargate)

Real-world usage:
* running microservices without managing Kubernetes complexity.
* internal APIs, background workers, event consumers.
* batch jobs and scheduled tasks.

As a DevOps engineer, you will:
* design task definitions (CPU, memory, env vars, secrets).
* connect services to ALBs/NLBs.
* configure autoscaling based on metrics.
* manage deployments and rollbacks.
ECS with Fargate is often the fastest way into containers on AWS.

## 17. EKS – Elastic Kubernetes Service
EKS is managed Kubernetes on AWS.

It gives you:
* a Kubernetes control plane
* you manage worker nodes (EC2 or Fargate) and workloads
  
Real-world usage:
* large-scale microservice architectures.
* teams already using Kubernetes on-prem moving to cloud.
* complex deployments requiring advanced control.
  
As a DevOps engineer, you will:
* provision and manage EKS clusters.
* deploy apps via Helm, Kustomize, or raw YAML.
* manage networking (CNI), ingress controllers, and storage.
* integrate EKS with ECR, IAM, and VPC.
EKS is a big topic, but extremely valuable in modern DevOps roles.

## 18. RDS – Relational Database Service
RDS gives you managed relational databases like:

MySQL, PostgreSQL, MariaDB, SQL Server, Oracle

AWS handles:
* backups
* patching
* basic high availability
* storage scaling
  
Real-world usage:
* main application databases.
* analytics workloads (with read replicas).
* internal tools and services.
  
As a DevOps engineer, you will:
* create RDS instances in private subnets.
* control access through security groups and IAM.
* manage backups, snapshots, and restores.
* tune performance and monitor metrics (connections, latency, IOPS).
RDS removes a lot of DBA overhead and is a core part of many architectures.

## 19. Elastic Load Balancer (ALB / NLB)
Load balancers distribute traffic across multiple targets (EC2, ECS, Lambda, IPs).

Types:
* ALB (Application Load Balancer): HTTP/HTTPS, path-based routing, host-based routing.
* NLB (Network Load Balancer): TCP/UDP, ultra-low-latency, suitable for high-performance needs.
  
Real-world usage:
* fronting web apps and APIs.
* routing /api to one service and /app to another.
* handling SSL termination.
  
As a DevOps engineer, you will:
* configure listeners, target groups, and health checks.
* integrate ALBs with ECS/EKS/EC2.
* manage SSL/TLS certificates.
* debug “502”, “504” and similar issues during deployments.
Load balancers are critical for building reliable, scalable apps.

## 20. CloudTrail & Config
These services give you history and visibility of what changed.

CloudTrail:
* records API calls and actions in your account.
* helps answer: “who did what and when?”
  
Config:
* tracks configuration of resources over time.
* checks if resources follow certain rules (e.g., all S3 buckets must be encrypted).
  
Real-world usage:
* auditing and investigations after incidents.
* compliance checks for security standards.
* alerting when someone changes critical configs.
  
As a DevOps engineer, you will:
* enable and store CloudTrail logs centrally (often in S3).
* define Config rules or use managed ones.
* work with security teams to review and act on findings.
These tools strengthen your governance and visibility.

## 21. AWS Migration Strategies
This is about moving existing systems into AWS.

Common patterns:
* Lift-and-shift: move apps to EC2 “as is”.
* Re-platform: move DBs to RDS, apps to ECS/EKS/Lambda.
* Re-architecture: redesign apps to be cloud-native.
  
Real-world usage:
* modernizing old apps.
* leaving data centers for cloud.
* step-by-step migration with minimal downtime.
  
As a DevOps engineer, you will:
* help design migration plans.
* build new infra in AWS.
* move data safely (DMS, backups/restores).
* support testing, cutover, and rollback plans.
This is where a lot of real-world, high-impact work happens.

## :hourglass_flowing_sand: Hands-On Projects (VERY IMPORTANT FOR INTERVIEWS)
Project 1 (Beginner)
* Run on AWS EC2
* Dockerize an app

Project 2 (Advanced)
* Deploy app on Kubernetes
* CI/CD pipeline
* Monitoring with Prometheus & Grafana

:point_right:These projects alone can clear many interviews.







