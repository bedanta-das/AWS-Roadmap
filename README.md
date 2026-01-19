# :cloud: AWS DevOps Roadmap – With Real-World Notes (2026)
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

## IAM – Identity and Access Management
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

## EC2 – Elastic Compute Cloud
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

