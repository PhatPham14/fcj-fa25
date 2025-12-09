---
title: "Event 3: DevOps on AWS Workshop"
date: 2025-11-17
weight: 1
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: “DevOps on AWS Workshop”

### Event Information

- **Time:** 08:30 – 17:00, Monday, November 17, 2025.
- **Location:** AWS Vietnam Office, Bitexco Financial Tower, District 1, HCMC.
- **Topic:** DevOps Culture, Automation (CI/CD), Infrastructure as Code (IaC), and System Monitoring.

### Objectives

- **Standardization:** Understand DevOps culture and efficiency metrics (DORA metrics) to apply to teamwork processes.
- **Automation:** Master AWS Developer Tools (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) to build a complete CI/CD pipeline.
- **Infrastructure Management:** Adopt Infrastructure as Code (IaC) thinking with AWS CDK for more efficient resource management.
- **Operations:** Learn how to monitor and trace errors (Observability) for Microservices applications.

### Key Content & Agenda

The full-day workshop covered intensive technical knowledge, divided into morning and afternoon sessions:

#### 1. Morning Session: DevOps Mindset & CI/CD (08:30 – 12:00)
- **DevOps Culture:** Understanding that DevOps is not just tools but a culture combining Development and Operations. Key metrics: MTTR (Mean Time To Recovery) and deployment frequency.
- **AWS CI/CD Pipeline:**
    - **Source Control:** Managing source code with AWS CodeCommit (and GitFlow strategies).
    - **Build & Test:** Configuring AWS CodeBuild to package applications.
    - **Deployment:** Safe deployment strategies (Blue/Green, Canary) with AWS CodeDeploy.
    - **Orchestration:** Automating the entire process using AWS CodePipeline.
- **IaC (Infrastructure as Code):** Comparison between CloudFormation (Templates) and AWS CDK (Code). Demo of infrastructure deployment using CDK.

#### 2. Afternoon Session: Containers & Observability (13:00 – 17:00)
- **Container Services:**
    - Managing Docker images with **Amazon ECR**.
    - Container orchestration with **Amazon ECS** and **EKS**.
    - Comparison of Microservices deployment on different platforms.
- **Monitoring & Observability:**
    - Setting up Dashboards and Alarms with **Amazon CloudWatch**.
    - Distributed tracing with **AWS X-Ray** to identify performance bottlenecks.
- **Best Practices:** Incident management strategies and AWS DevOps certification roadmap.

### Key Highlights & Takeaways

#### IaC is a "Game Changer"
- Previously, my team often created resources by clicking on the Console (ClickOps), which is prone to errors and hard to synchronize. Through the **AWS CDK** demo, I realized the power of defining infrastructure using programming languages (TypeScript/Python). This makes reproducing environments (Dev/Test/Prod) easy and absolutely accurate.

#### CI/CD is more than just Deploying Code
- I learned that a standard pipeline is not just pushing code to the server, but must include **Automated Testing** and **Safe Deployment** strategies (like Blue/Green) to minimize downtime risks for end-users.

#### Observability > Monitoring
- Monitoring only tells you "The system is broken", while Observability (with X-Ray) tells you "Why it broke". With the current project's Microservices architecture, integrating X-Ray is mandatory for effective debugging.

### Event Photos

![CI/CD Pipeline Demo](/images/4-Events/devops-workshop-1.jpg)
*(Complete CI/CD Pipeline model on AWS)*

![CDK Practice](/images/4-Events/devops-workshop-2.jpg)
*(Infrastructure deployment demo using AWS CDK)*

![CloudWatch Dashboard](/images/4-Events/devops-workshop-3.jpg)
*(Full-stack system monitoring interface)*

### Personal Reflection

The **DevOps on AWS** workshop was the final crucial technical piece I was missing for the Group Project.

It helped me systematize the entire software development process. Immediately after the session, I had ideas to refactor the team's current GitLab CI pipeline, integrating ECR security scanning and X-Ray tracing to best prepare for the upcoming Final Showcase.

> **Conclusion:** A day flooded with knowledge but incredibly valuable. I am now more confident to say that I understand standard DevOps processes!