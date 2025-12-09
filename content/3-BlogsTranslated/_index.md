---
title: "Translated Blogs"
date: 2025-10-07 
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section lists and introduces the technical blogs I have translated and studied during the internship. These articles cover various topics including Data Analytics, High Performance Computing (HPC), IoT, and Security.

### [Blog 1 - Getting started with healthcare data lakes: Using microservices](3.1-Blog1/)
This blog introduces how to build a healthcare data lake using a microservices architecture. You will learn the importance of storing and analyzing diverse healthcare data (EMR, lab tests, IoT) and how microservices offer flexibility and scalability. The article guides you through setting up an ingestion pipeline for HL7v2 messages using AWS Lambda, Amazon SNS, and DynamoDB.

### [Blog 2 - Characteristics of Financial Services HPC Workloads on the Cloud](3.2-Blog2/)
This article analyzes the technical attributes of compute-heavy workloads in the Financial Services Industry (FSI). It provides a decision tree to help organizations choose the right HPC platform on AWS—whether migrating existing commercial schedulers (like IBM Symphony) or building cloud-native solutions using AWS Batch or AWS Lambda—based on task duration and throughput requirements.

### [Blog 3 - AWS IoT Greengrass Nucleus Lite](3.3-Blog3/)
Introduces Nucleus Lite, a lightweight, C-based edge runtime optimized for resource-constrained devices (under 512MB RAM). The blog compares it with the standard Java Nucleus runtime, highlighting benefits like reduced memory footprint, static memory allocation, and deep integration with systemd for embedded Linux systems.

### [Blog 4 - Proactive Strategies for Cyber Resilience and Business Continuity](3.4-Blog4/)
Provides guidance for Public Sector organizations to operate resilient systems. It covers essential strategies such as implementing a multi-account environment, using Infrastructure as Code (IaC) for rapid recovery, maintaining separate recovery accounts with consistent Availability Zone IDs, and utilizing immutable backups to defend against ransomware.

### [Blog 5 - The Frugal HPC Architect: Effective FinOps for HPC](3.5-Blog5/)
Explores best practices for managing costs in large-scale HPC workloads. Based on the "Frugal Architect" principles, it discusses strategies to reduce unit costs (using EC2 Spot, Savings Plans, and Graviton processors) and unit consumption (optimizing efficiency and observability) to balance flexibility, performance, and budget.