---
title: "Event 4: AWS Well-Architected Security Pillar Workshop"
date: 2025-11-29
weight: 1
chapter: false
pre: " <b> 4.4. </b> "
---

# Summary Report: “AWS Well-Architected Security Pillar Workshop”

### Event Information

- **Time:** 08:30 – 12:00, Saturday, November 29, 2025 (Morning Only).
- **Location:** AWS Vietnam Office, Bitexco Financial Tower, District 1, HCMC.
- **Topic:** Comprehensive Cloud Security based on the AWS Well-Architected Framework.

### Objectives

- **Reinforce Security Mindset:** Deeply understand the 5 pillars of security (Identity, Detection, Infrastructure, Data, Incident Response).
- **Practical Application:** Learn how to design systems adhering to "Zero Trust" and "Defense in Depth" principles.
- **Future Preparation:** Grasp the roadmap for advanced security certifications (AWS Security Specialty).

### Key Content & Agenda

The workshop focused heavily on Security Best Practices, divided into in-depth sessions:

#### 1. Security Foundation (08:30 – 08:50)
- **Core Principles:** Least Privilege, Zero Trust, and Defense in Depth.
- **Shared Responsibility Model:** Clearly understanding the boundary of responsibility between AWS and the customer.
- **Landscape:** Top common security threats in the Vietnamese enterprise environment.

#### 2. The Five Security Pillars (08:50 – 11:40)
* **Pillar 1 - Identity & Access Management (IAM):**
    * Transitioning from IAM Users to **IAM Identity Center** (SSO).
    * Using SCPs and Permission Boundaries for Multi-account management.
    * **Demo:** Simulating access and validating IAM Policies.
* **Pillar 2 - Detection:**
    * Continuous monitoring with **GuardDuty** and **Security Hub**.
    * Automated Alerting using EventBridge.
* **Pillar 3 - Infrastructure Protection:**
    * Network protection with WAF, Shield, and Network Firewall.
    * VPC Segmentation and Security Groups vs. NACLs models.
* **Pillar 4 - Data Protection:**
    * Encryption key management with **KMS** (Key rotation, policies).
    * Protecting sensitive secrets with **Secrets Manager**.
* **Pillar 5 - Incident Response (IR):**
    * IR Lifecycle according to AWS.
    * Building Playbooks for scenarios: Compromised IAM keys, S3 public exposure, EC2 malware.

### Key Highlights & Takeaways

#### Identity is the New Perimeter
- Previously, I focused mostly on Network Firewalls, but this workshop emphasized that in the Cloud, **Identity** is the most critical security layer. Strictly managing IAM Roles and Policies is the first and most effective line of defense.

#### Automated Incident Response (IR Automation)
- The concept of **"Automated Response"** was truly impressive. Instead of waiting for human intervention during an incident, we can use Lambda functions to automatically isolate an infected EC2 instance or immediately revoke a compromised IAM key.

#### Security Should Not Slow Down Development
- The "Security as Code" message helped me understand that security should be integrated into the DevOps process (DevSecOps) from the beginning, rather than being a bottleneck at the last minute.

### Event Photos

![Participating in Event](/images/4-Events/E4.jpeg)

### Personal Reflection

Even though it took place on a Saturday morning after completing the Final Showcase, this workshop still attracted my full participation due to its importance.

Security knowledge is often dry, but the approach through practical Playbooks (such as handling S3 bucket exposure) made the lessons very accessible. This provides a solid foundation for me to be more confident when joining real-world enterprise projects after the internship, where security is always a top priority.

> **Conclusion:** A perfect ending to the technical training series, completing the final piece of a Cloud Engineer: **Security**.