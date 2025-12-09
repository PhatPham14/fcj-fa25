---
title: "Proactive Strategies for Cyber Resilience and Business Continuity on AWS"
date: 2025-07-11
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
tags:
  - AWS Public Sector
  - Best Practices
  - Disaster Response
  - Security
---

**By Devin Gordon and Henrik Balle**

![pic 1](/images/3-Blog/B3-1.png)

[Amazon Web Services (AWS)](https://aws.amazon.com/) recommends that organizations prepare to recover workloads in the event of cybersecurity incidents or business continuity events such as natural disasters or technical failures. In this post, we provide guidance and strategies for Public Sector organizations to use AWS infrastructure to operate resilient systems in the cloud.

AWS recommends that its customers:
* Use cybersecurity frameworks and AWS architectural best practices.
* Implement a multi-account environment.
* Use [infrastructure as code (IaC)](https://aws.amazon.com/what-is/iac/) to deploy AWS environments and workloads.
* Prepare a recovery account in an Availability Zone or [Region](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region) different from the primary workload.
* Include all application code, IaC code, configuration files, and other dependencies in the recovery account.
* Define a data backup strategy to the recovery account.
* Implement automated testing (unit and full workload) in the recovery account.

---

### Use an established framework

As cybersecurity incidents like ransomware increase, Public Sector organizations look to frameworks such as the [NIST Cybersecurity Framework (CSF) 2.0](https://www.nist.gov/cyberframework) from the [National Institute of Standards and Technology (NIST)](https://www.nist.gov/) to guide better cybersecurity risk governance. While the CSF organizes cybersecurity outcomes by functions (govern, identify, protect, detect, respond, recover), NIST does not prescribe specific ways to achieve those outcomes.

For more specific guidance, refer to resources such as:
* **[AWS Blueprint for Ransomware Defense](https://d1.awsstatic.com/whitepapers/compliance/AWS-Blueprint-for-Ransomware-Defense.pdf):** Provides a mapping of AWS services to CSF functions.
* **[AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/):** Dives into six pillars to help cloud architects build secure, high-performing, resilient, and efficient infrastructure, following the [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/).

These frameworks are complemented by the [AWS Security Reference Architecture (AWS SRA)](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/welcome.html), which helps you design, deploy, and manage AWS security services.

---

### Implement a multi-account strategy on AWS

AWS recommends following best practices when deploying cloud environments by using a multi-account strategy, also known as a [landing zone](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-aws-environment/understanding-landing-zones.html). Using [AWS Organizations](https://aws.amazon.com/organizations/) along with [AWS Control Tower](https://aws.amazon.com/controltower/) or [Landing Zone Accelerator on AWS](https://aws.amazon.com/solutions/implementations/landing-zone-accelerator-on-aws/) creates an environment suitable for management and automation. This helps isolate and manage applications and data, and eliminate unintended lateral movement.

In a multi-account strategy, AWS recommends centrally managing identities using [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/).
> **Note:** In a recovery scenario, you may need to [use root credentials](https://docs.aws.amazon.com/managedservices/latest/userguide/how-when-to-use-root.html). Root credentials should be properly secured to prevent account takeover. AWS [recently announced](https://aws.amazon.com/blogs/aws/centrally-managing-root-access-for-customers-using-aws-organizations/g-aws-organizations/) new capabilities for centrally managing root credentials to strengthen security posture.

---

### Build your AWS infrastructure with automation

As a key principle of DevSecOps, AWS recommends deploying all AWS infrastructure using **Infrastructure as Code (IaC)**. IaC helps iterate infrastructure quickly, improve consistency, reduce configuration errors, and crucially serves as documentation for infrastructure to accelerate recovery.

Supporting tools and services:
* **[AWS CloudFormation](https://aws.amazon.com/cloudformation/):** Define infrastructure using templates. You can also [create a stack from existing infrastructure](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import-new-stack.html).
* **[AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/):** Define resources using programming languages.
* **[AWS Serverless Application Model (AWS SAM)](https://aws.amazon.com/serverless/sam/):** An open-source framework for serverless applications.
* **[HashiCorp Terraform](https://developer.hashicorp.com/terraform):** A multi-platform IaC tool.

IaC code should be stored in a source code repository (e.g., GitLab). You can use the [DevOps Pipeline Accelerator (DPA)](https://github.com/aws-samples/aws-devops-pipeline-accelerator) to build a standardized CI/CD pipeline.

---

### Prepare a recovery location

AWS recommends establishing separate accounts dedicated to recovery to deal with cybersecurity incidents.

To deal with technical failures or natural disasters (e.g., [AWS Availability Zone](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-availability-zones.html) outage):
* If using the same Region, ensure the AZ used for recovery is discrete from the primary workload.
* Use **Availability Zone IDs (AZ IDs)** to ensure consistency across accounts (since AWS randomizes AZ names between accounts).

![pic 1](/images/3-Blog/B3-2.png)
> *Figure 1. Example of workload and recovery account using Availability Zone ID.*

For higher fault tolerance, consider **multi-Region recovery**. For example: Primary Region in *US East (N. Virginia)* and backup in *US East (Ohio)*. Evaluate your encryption key strategy with [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) to decrypt cross-region backup data.

---

### Define a backup strategy and implement automated testing

AWS recommends aligning your backup strategy with cloud-based solutions:
* Use **[AWS Backup](https://aws.amazon.com/backup/)** to back up workload data, IaC, infrastructure configuration, application code, and [AMIs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html) to the recovery account.
* Consider an **Immutable backup** strategy with [AWS Backup Vault Lock](https://aws.amazon.com/blogs/storage/protecting-data-with-aws-backup-vault-lock/) to protect against ransomware.

**Automated Testing:**
After setting up the recovery account, implement automated testing to validate the viability of backup data. You should periodically build the full workload in the recovery account using IaC code and backups to ensure the Business Continuity process runs smoothly.

---

### Conclusion

By following the best practices in this post, Public Sector organizations can use AWS capabilities to prepare for recovery from a business continuity event. Please contact your AWS account team and solutions architect for further guidance.

---

#### About the Authors

> **Devin Gordon**
>
> Principal Solutions Architect at Amazon Web Services (AWS), supporting federal civilian agencies. He specializes in security on AWS and is passionate about helping customers deploy secure environments while leveraging emerging technologies. He enjoys SCUBA diving and rock climbing.

> **Henrik Balle**
>
> Principal Solutions Architect at AWS, supporting the US public sector. He works closely with customers on a wide range of topics from machine learning to security and governance at scale. He enjoys road biking and home renovation projects.