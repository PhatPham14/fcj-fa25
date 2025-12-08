---
title: "Week 7 Worklog"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives

- Understand and apply **data and system security practices** in AWS.  
- Configure, manage, and optimize **Amazon VPC (Virtual Private Cloud)** for secure private networking.  
- Learn how to **back up, restore, and implement Disaster Recovery (DR)** using AWS services.  

**Time Period:** 10/11/2025 - 16/11/2025

---

### Weekly Task Overview

| Day | Activity                                                                                                                                                                                                                                                           | Start Date   | End Date     | Reference                               |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ------------ | ---------------------------------------- |
| 1   | - Begin writing the project **Proposal** <br> + Complete the **Executive Summary**, **Problem Statement**, and **Overall System Architecture** <br> + Research AWS services to be integrated in later deployment phases                                            | 2025-11-10    | 2025-11-10   | -                                        |
| 2   | - Build **Domain → Persistence → Application Layer** for the Mini-Market system <br> + Create entities <br> + Implement **Repository & Unit of Work Pattern** <br> + Run migrations & seed data <br> + Develop core business logic services                         | 2025-11-11    | 2025-11-11   | -                                        |
| 3   | - Initialize the **WebShop MVC** project <br> + Create base layout (Header, Footer, Navigation) <br> + Build **Product List – Shopping Cart** pages <br> + Write the **Architecture & Technical Implementation** section of the Proposal                             | 2025-11-12    | 2025-11-12   | -                                        |
| 4   | - Draw the **AWS Architecture Diagram** for the system <br> + Collect information for each service used: <br> &emsp; · Elastic Beanstalk <br> &emsp; · RDS SQL Server <br> &emsp; · Amazon S3 <br> &emsp; · CloudFront <br> &emsp; · WAF & Route 53 <br> &emsp; · ElastiCache Redis <br> &emsp; · NAT Gateway <br> &emsp; · CodePipeline/CodeBuild | 2025-11-13    | 2025-11-13   | -                                        |
| 5   | - Study **Disaster Recovery & Backup** <br> + Use **AWS Backup** for automated resource backup <br> + Configure **RDS Read Replicas** for improved fault tolerance <br> + Practice **Cross-Region Failover** for DR planning                                         | 2025-11-14    | 2025-11-14   | <https://aws.amazon.com/backup/>         |
| 6   | - Summarize project progress and update the Proposal <br> + Review architecture, IAM roles, and selected AWS services <br> + Prepare content for Week 8: S3 upload integration, Redis caching, and architecture optimization                                      | 2025-11-15    | 2025-11-15   | -                                        |

---

### Week 7 Achievements

- Strengthened knowledge of **AWS security and data encryption**:
  - Practiced creating and managing **KMS keys** for data protection.  
  - Understood how **CloudHSM** enhances hardware-level key security.  
  - Configured **AWS Shield** and **WAF** to safeguard applications from DDoS attacks and malicious traffic.  

- Gained solid understanding of **Amazon VPC networking**:
  - Created and configured **VPC**, **subnets**, **route tables**, **Internet Gateway**, and **NAT Gateway**.  
  - Applied **Security Groups** and **Network ACLs** for effective access control.  
  - Set up **VPN Connection** and studied **Direct Connect** for secure, high-throughput connectivity.  

- Mastered core concepts of **Disaster Recovery (DR)** and data backup:
  - Used **AWS Backup** for automated scheduled backups.  
  - Configured **RDS Read Replicas** to ensure data availability.  
  - Practiced **Cross-Region Failover** to maintain system continuity during outages.  

- Improved ability to design **secure, reliable, and highly resilient** AWS architectures:
  - Learned to integrate **Security**, **Networking**, and **Resilience** best practices.  
  - Prepared foundational knowledge for next week’s topics: **Automation, Infrastructure as Code (IaC), and DevOps Practices**.

