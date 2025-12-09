---
title: "Characteristics of Financial Services HPC Workloads on the Cloud"
date: 2025-04-15
weight: 10
chapter: false
pre: " <b> 2.1. </b> "
tags:
  - FSI
  - HPC
  - Best Practices
---

**By Mark Norton and Flamur Gogolli**

This post introduces the requirements of High Performance Computing (HPC) in the Financial Services Industry (FSI). It defines the technical attributes of compute-heavy workloads and provides a decision tree process to help customers select the right HPC platform on AWS.

---

### HPC in Financial Services

In the financial services sector, HPC (also known as Grid computing) has long been used to run simulations and solve complex challenges.

* **Capital Markets:** Pricing financial instruments (stocks, ETFs, derivatives, bonds) using mathematical models like Monte Carlo. Workloads range from real-time/intraday latency-sensitive calculations to large batch workloads running overnight for risk monitoring.
* **Investment Management:** Risk analysis, exposure calculation, and strategy optimization/back-testing.
* **Insurance:** Actuarial modeling and catastrophe simulations to determine premiums and risk mitigation strategies.

---

### Cloud Adoption Patterns in FSI

Financial institutions often migrate their HPC platforms to the cloud in phases to address fluctuating resource demands (e.g., end-of-quarter reporting).



Here are the common cloud adoption levels:

1.  **All On-premises:** Scheduler, compute, and data are hosted entirely on-site.
2.  **Hybrid Burst:** Scheduler remains on-premises, but compute capacity bursts to the cloud during peak demand.
3.  **Lift and Shift:** The existing scheduler and compute nodes are moved "as-is" to the cloud.
4.  **AWS Optimized:** Focuses on compute elasticity, using managed services, and optimizing purchase models (Spot, Savings Plans).
5.  **AWS Native:** Complete re-imagining using cloud-native architectures, serverless building blocks, and optimized hardware (AI accelerators, next-gen chips).

---

### Workload Characteristics for Architecture Decisions

To select the right platform, consider the following workload attributes:

* **Task Duration:** Ranging from seconds to days.
* **High Throughput:** Requirements often reach tens of thousands of tasks per second.
* **Parallelization:** Loosely coupled calculations allowing parallel execution.
* **Resource Intensity:** CPU/Memory/IO ratios.
* **Software Requirements:** OS, libraries, dependencies.
* **Cost Optimization:** Balancing performance vs. resource efficiency.

Use the decision tree below to guide your platform selection:



> *Figure 1. Decision tree for selecting an HPC solution on the cloud based on workload characteristics.*

The critical decision starts with: **Migrating an existing Scheduler** vs. **Building a new Cloud-native solution**.

---

### 1. Migrating Your Existing Scheduler to the Cloud

If you choose to keep your existing Grid scheduler due to migration effort concerns or project timelines:

* **Commercial Schedulers:** IBM Spectrum Symphony, TIBCO DataSynapse GridServer®.
* **Open-source Schedulers:** Slurm Workload Manager, HTCondor.

Common approaches include **Hybrid Burst** or **Lift-and-Shift**. While offering a familiar interface, this approach retains legacy limitations regarding licensing and complex infrastructure management.

### 2. Building and Using a Cloud-Native HPC Scheduler

This approach reduces operational burden and maximizes cloud benefits. The decision is heavily influenced by **Task Duration**:

#### A. Mixed Short and Long Tasks (Seconds to Minutes)
* **Slurm on AWS:** Use **AWS ParallelCluster** (open-source cluster management) or **AWS Parallel Computing Service** (fully managed).

#### B. Long Tasks (> 1 Minute)
* **AWS Batch:** Fully managed batch computing service. The scheduler is free; you only pay for the compute resources used.

#### C. High Throughput (Seconds to Minutes)
* **HTC-Grid:** A community project (originally an AWS blueprint, now part of FINOS) designed for high-throughput processing of tens of thousands of tasks per second.

#### D. Short Tasks (< 15 Minutes)
* **AWS Lambda:** Leverage serverless architecture. No "always-on" server management is required; ideal for high throughput but subject to strict execution time limits.



---

### Conclusion & Key Takeaways

There is no "one-size-fits-all" solution. Your choice depends on your strategy:

1.  **Maintaining Existing Schedulers:**
    * *Commercial:* IBM Symphony, Tibco (Enterprise reliability but may lack flexibility).
    * *Open-source:* Slurm, HTCondor (Use AWS ParallelCluster for easier management).

2.  **Moving to Cloud-Native:**
    * *Workloads > 5 minutes:* **AWS Batch**.
    * *Workloads < 15 minutes:* **AWS Lambda**.
    * *High throughput (seconds-minutes):* **HTC-Grid** or custom container-based solutions.

Ideally, view this decision as the start of a journey. Customers often progress "down the stack" from "Lift & Shift" to "AWS Native" over time.

---

#### About the Authors

> **Mark Norton**
>
> Principal HPC Specialist at AWS with over 30 years of experience. He specializes in designing scalable cloud solutions for the financial, automotive, and research sectors.

> **Flamur Gogolli**
>
> Senior Specialist Solutions Architect at AWS. Formerly with JP Morgan, he has extensive experience in infrastructure modernization, Cloud-native architectures, Containers, and DevOps.