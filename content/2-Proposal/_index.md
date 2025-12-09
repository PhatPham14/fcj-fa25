---
title: "Proposal"
date: "2025-11-05"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# APEX-EV Electric Vehicle Service Platform 

### 1. Executive Summary
RenGen is a comprehensive management platform designed to digitize and optimize maintenance workflows at service centers. The system centrally manages the entire service lifecycle—from request intake and repair processing to customer care—helping to eliminate manual tasks and enhance efficiency. Leveraging the power of the AWS cloud, RenGen combines flexible container architecture on Amazon ECS Fargate with the intelligent processing capabilities of Generative AI through Amazon Bedrock. The solution integrates automated development processes (CI/CD) from GitLab, ensuring rapid deployment speeds, high security, and rigorous monitoring, delivering a superior experience for end-users.

### 2. Problem Statement
### What’s the Problem?
Current operational processes rely heavily on manual methods, leading to inefficiencies, fragmented data, and a lack of intelligent support tools for automated customer interaction.

### The Solution
The platform employs a modern architecture, starting at the Edge layer with Amazon Route 53 for user routing. The interface (Frontend) is hosted on AWS Amplify Hosting, ensuring fast and stable access.
Amazon API Gateway acts as the central hub, intelligently routing requests.

To ensure security, critical components such as ECS Fargate and the Amazon RDS database are placed in a Private Subnet, completely isolated from the public internet. Image data is stored on Amazon S3 and accessed securely via S3 Endpoints. Additionally, the software development process is fully automated: source code from GitLab is packaged and pushed to Amazon ECR for deployment to ECS.

### Benefits and Return on Investment
Adopting this architecture delivers a significant competitive advantage by integrating Artificial Intelligence (GenAI) via Amazon Bedrock, which helps automate customer care and data analysis. The system ensures high availability and data security thanks to the VPC network separation design (Public/Private subnets).

The CI/CD process integrated with GitLab and ECR helps minimize downtime when updating new features, while Amazon CloudWatch provides comprehensive monitoring to detect incidents instantly. The cost model is optimized thanks to the use of Fargate (Serverless container) and Lambda (Pay-per-use), ensuring businesses only pay for the actual resources used. This investment not only resolves current operational challenges but also creates a solid technological foundation for long-term growth, with the expected Return on Investment (ROI) period significantly shortened.

### 3. Solution Architecture
The RenGen management platform utilizes a modern architecture deployed on AWS (Region **ap-southeast-2**), initiated by user access via **Amazon Route 53** at the Edge layer. The User Interface (Frontend) is hosted on **AWS Amplify Hosting**, which establishes a direct connection to **Amazon API Gateway** as the central entry point.

From the API Gateway, the data flow is strategically divided into three distinct paths:

* **AI Tasks:** Requests are routed to **AWS Lambda** to interact with **Amazon Bedrock** for generative AI capabilities.
* **Notification Tasks:** Asynchronous requests trigger **AWS Lambda** to handle email communications via **Amazon SES**.
* **Core Business Logic:** Traffic is directed through an **Application Load Balancer (ALB)** located in the Public Subnet, then forwarded to **Amazon ECS Fargate** instances secured within a Private Subnet.

**Data & Security:**

Relational data is persistently stored in **Amazon RDS** within the Private Subnet. To optimize security and performance, the architecture utilizes **VPC Endpoints** to keep traffic strictly within the AWS internal network:

* Static assets and images stored in **Amazon S3** are accessed securely via **S3 Endpoints**.
* Container images are pulled directly from **Amazon ECR** via **ECR Endpoints**.

By leveraging these endpoints, the system eliminates the need for a NAT Gateway, thereby reducing costs and minimizing public internet exposure.

**DevOps & Monitoring:**

* **GitLab** is used for source code management and CI/CD, automatically pushing deployments to Amplify (Frontend) and container images to ECR (Backend).

![APEX-EV Platform Architecture](/images/2-Proposal/RengenZ.jpg)

### AWS Services Used
- *Route 53*: DNS service, responsible for routing the domain (Edge layer) to the application. 
- *AWS Amplify Hosting*: Hosts the web interface (frontend) and can integrate with CDN/WAF. In the diagram, it receives traffic from Route 53.
- *Amazon API Gateway*: The main entry point (Gateway), receiving and routing all requests from the frontend/Amplify to processing services.  
- *AWS Lambda (Bedrock)*: Handles AI/Generative AI tasks (prediction/content generation) by communicating with Amazon Bedrock.
- *AWS Lambda (SES)*: Handles asynchronous tasks, such as processing notifications to send emails via AWS SES.
- *Amazon Bedrock*: General AI service (Gen AI), providing foundation models to execute intelligent business operations.
- *AWS SES*: Email sending service, performs the sending of notifications, quotes, or processing results from Lambda.
- *VPC*: Virtual network environment containing and protecting AWS resources (like ALB, ECS Fargate, RDS).
- *ALB (Application Load Balancer)*: Load balancer, distributing traffic from API Gateway to application containers running on ECS Fargate.
- *Amazon ECS Fargate*: Runs the backend application as containers without server management, handling core business logic.
- *Amazon RDS*: Provides a relational database, placed in a Private Subnet to store structured data.
- *Amazon S3*: Stores multimedia files like photos or other large data.
- *ECR*: Repository for application container images (Docker), used by ECS Fargate for deployment.
- *AWS CloudWatch*: Monitoring service, collecting logs and metrics from the entire system to track performance and detect issues.

### Component Design

* **Request Handling:**
    **Amazon Route 53** routes user domain requests to **AWS Amplify Hosting**, where the frontend interface is hosted. From there, API requests are forwarded to **Amazon API Gateway**, which acts as the central entry point to receive and route all incoming traffic.

* **Business Logic Processing:**
    * **Core Logic:** All primary business operations are handled by containerized applications running on **Amazon ECS Fargate**, deployed within a Private Subnet to ensure maximum security.
    * **AI & Asynchronous Tasks:** Generative AI tasks are processed by **AWS Lambda** interacting with **Amazon Bedrock**. Auxiliary tasks, such as email notifications, are handled by separate **AWS Lambda** functions triggering **Amazon SES**.

* **Network Infrastructure:**
    * **Public Subnet:** Hosts the **Application Load Balancer (ALB)** to receive and distribute external traffic.
    * **Private Subnet:** Dedicated to sensitive resources including ECS Fargate and Amazon RDS, ensuring they are isolated from direct public internet access.
    * **VPC Endpoints:** The system explicitly utilizes **S3 Endpoints** and **ECR Endpoints**. This design allows ECS Fargate to pull container images and access file storage securely within the AWS internal network, **without traversing the public internet**.

* **Data Storage:**
    * **Amazon RDS:** Stores sensitive, structured relational data.
    * **Amazon S3:** Stores multimedia files and large datasets.

* **Deployment and Monitoring:**
    The deployment pipeline is managed via **GitLab**, which triggers updates to AWS Amplify (Frontend) and pushes Docker images to **Amazon ECR** (Backend). **Amazon CloudWatch** provides comprehensive monitoring of performance logs and metrics across all services, from ECS and Lambda to RDS.

### 4. Technical Implementation
**Implementation Phases**
The development project for the RenGen Smart Electric Vehicle Maintenance Platform — including the integration of an AI virtual assistant and a service management system — undergoes 4 phases:
1. *Research and Architectural Design*: Research suitable technologies (React.js, Spring Boot, AWS Bedrock) and design a system architecture combining Containers (ECS) and Serverless (Lambda) on AWS (1 month prior to commencement).
2. *Cost Estimation and Feasibility Check*: Use the AWS Pricing Calculator to estimate operating costs for core services such as ECS Fargate, RDS, and token costs for Amazon Bedrock, and propose the most feasible solution.
3. *Architecture Adjustment for Cost/Solution Optimization*: Refine the architecture, select appropriate configurations for ECS Fargate and RDS, and optimize Lambda runtime (timeouts) to balance AI processing performance and cost.
4. *Development, Testing, and Deployment*: Program the React.js application (Frontend) and Spring Boot (Backend), integrate the Bedrock Agent, deploy CI/CD pipelines via GitLab, package Docker images to ECR, and launch operations on ECS. Technical Requirements
*Technical Requirements*  
- *User Interface (Frontend)*: Practical knowledge of React.js to build scheduling interfaces and chat with the AI virtual assistant. Use AWS Amplify to automate the deployment process (Hosting), connect with Amazon API Gateway to send secure processing requests, ensuring a smooth user experience on all devices.
- *Core System (Backend & Infrastructure)*: In-depth knowledge of Java/Spring Boot to develop maintenance business logic. The application is packaged using Docker, with images stored on AWS ECR and running on Amazon ECS Fargate. Requires understanding of Amazon RDS for relational databases (storing vehicle profiles, maintenance history). Specifically, requires AWS Lambda (Python) programming skills to connect with Amazon Bedrock (AI/Chatbot processing) and AWS SES (sending asynchronous email notifications). Manage detailed user authentication and authorization (customers/technicians) via Amazon Cognito.

### 5. Timeline & Milestones
**Project Timeline**
1. *Phase 1 (Week 1-2): Design and Foundation:*:
- Analyze & Design detailed AWS architecture (VPC, Subnets, Security Groups). Design Database (RDS Schema) and define APIs (Swagger/OpenAPI).
- Configure infrastructure environment: Setup VPC (Public/Private Subnets), IAM Roles, and Amazon Cognito (User Pools).
- Setup CI/CD: Configure Pipeline on GitLab to automatically build Docker Images, push to Amazon ECR, and deploy Frontend to AWS Amplify.
2. *Phase 2 (Week 3-4): Core Service Flow Development:*: 
- Develop Customer flow (Frontend/Backend): Registration/Login, Vehicle Profile Management, Appointment Scheduling (stored in RDS).
- Develop Service Advisor flow: Vehicle Reception, Create Quotations and Repair Orders.
- Phát triển luồng Kỹ thuật viên: Xem danh sách việc cần làm (Task list), Cập nhật tiến độ bảo dưỡng và tải ảnh/video lên Amazon S3.
3. *Phase 3 (Week 5-6): Administration & Advanced Feature Development:*: 
- Build Administration Module: Report Dashboard, Spare Parts Management (Inventory), and Personnel Management.Build Administration Module: Report Dashboard, Spare Parts Management (Inventory), and Personnel Management.
- Write AWS Lambda to connect Amazon Bedrock Agent (AI Chatbot for customer support) and expose via API Gateway.
- Write AWS Lambda to trigger AWS SES for sending automatic notification emails/quotations to customers.
- Configure NAT Gateway so resources in Private Subnet (Lambda, ECS) can securely connect to the Internet/AWS Services.
4. *Phase 4 (Week 7-8): Testing, Optimization, and Operation:*:  
- Internal User Acceptance Testing (UAT) to ensure the flow from Web -> API Gateway -> Lambda/ECS -> DB operates smoothly.
- Optimize security: Configure AWS WAF (block SQL Injection, XSS) and review IAM access rights.
- Operational monitoring: Setup Dashboard on Amazon CloudWatch to track logs and metrics of ECS Fargate and Lambda.
- Official deployment.
### 6. Budget Estimation
**Infrastructure Costs**

- Amazon ECS Fargate: ~11.00 USD/month.
- Application Load Balancer (ALB): ~16.43 USD/month.
- Amazon Bedrock (AI): ~5.00 USD/month (Calculated by Token count).
- AWS Lambda: 0.00 USD/month (Free Tier).
- Amazon RDS & ElastiCache: 0.00 USD/month (Free Tier).
- S3 Standard: ~0.15 USD/month.
- AWS Amplify & API Gateway: ~0.50 USD/month.
- Amazon CloudWatch: 0.00 USD/month (Free Tier).
- Amazon SES: 0.00 USD/month (Free Tier).

*Total:* ~32.63/month.

### 7. Risk Assessment
#### Risk Matrix
- System downtime: High impact, low probability.
- Security breach/Data loss: Very high impact, low probability.
- Operational cost overrun: Medium impact, medium probability.
#### Mitigation Strategies
- System: Deploy infrastructure across Multi-AZ for RDS and ECS Fargate. Use Application Load Balancer for automatic load distribution and recovery.
- Security: Use AWS WAF to filter malicious requests. Strict authorization with Amazon Cognito and apply least privilege principle. Backend placed in a separate network (Private Subnet).
- Cost: Use AWS Budgets to set alerts when costs exceed thresholds. Regularly monitor and optimize resources (right-sizing) to avoid waste.
- Incorrect AI response: Medium impact, medium probability.
#### Contingency Plans
- System: Deploy ECS Fargate and RDS infrastructure across Multi-AZ to ensure high availability. Use Application Load Balancer for automatic load coordination and Auto-scaling to expand Tasks when traffic spikes.
- AI Quality: Limit Bedrock Agent response scope via strict Prompt Engineering (System Prompts) and only allow information retrieval from moderated Knowledge Bases.
- Enable Automated Backups for RDS and Point-in-time Recovery to restore data to any point in time.

### 8. Expected Outcomes
#### Technical Improvements: 
Technical Improvements: Successfully build a modern Hybrid Architecture combining Microservices (ECS Fargate) and Serverless (Lambda, Bedrock), ensuring flexible scalability without managing physical servers.

#### Long-term Value
Enhance customer experience: AI virtual assistant operating 24/7 helps reduce waiting time, increasing appointment conversion rates and car owner satisfaction.

Data assets: Maintenance history and interaction behavior data are centrally stored on RDS/S3, creating a premise for deploying AI Predictive Maintenance models for electric vehicle batteries and motors in the future.