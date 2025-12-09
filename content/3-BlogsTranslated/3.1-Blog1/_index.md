---
title: "Characteristics of Financial Services HPC Workloads on the Cloud"
date: 2025-04-15
weight: 10
chapter: false
pre: " <b> 3.1. </b> "
tags:
  - FSI
  - HPC
  - Best Practices
---

**By Mark Norton and Flamur Gogolli**

This post introduces the High Performance Computing (HPC) requirements in the Financial Services Industry (FSI). It defines the technical attributes of compute-heavy workloads and discusses their essential characteristics. Additionally, it provides a decision tree process to help customers select the right HPC platform on the cloud—whether commercial, open-source, or a cloud-native solution—based on customer and workload requirements.

While it cannot cover every possible option, this article provides guidance on how to achieve price-performance goals and solve HPC challenges using AWS services and solutions, based on experience with Financial Services customers.

In the financial services sector, HPC (also known as Grid computing) has long been used to run simulations and solve complex challenges.
* **Capital Markets:** HPC systems are used to price financial instruments (e.g., stocks, ETFs, derivatives, bonds) using mathematical models like [Monte Carlo](https://aws.amazon.com/what-is/monte-carlo-simulation/). Utilization models range from latency-sensitive real-time/intraday calculations to large batch workloads that typically run overnight to generate results for internal risk monitoring and regulatory reporting.
* **Investment Management:** HPC is used for pricing and risk analysis, exposure calculation, and the definition, optimization, and back-testing of hedging strategies.
* **Insurance:** HPC use cases include actuarial modeling and catastrophe simulations to help insurers understand losses, set premium levels, and develop risk mitigation strategies.

---

### Cloud adoption patterns in FSI

Financial institutions face increasing demand for HPC resources due to regulatory requirements, market volatility, and reporting needs—requiring massive capacity during periods like overnight processing or end-of-quarter reporting.

Many organizations are moving from on-premises infrastructure to the cloud to scale resources up and down on demand while optimizing costs. FSI customers typically migrate their HPC platforms to the cloud in phases:

* **All On-premises:** Scheduler, compute, and data sources are hosted on-site.
* **Hybrid Burst:** Scheduler, compute, and data remain on-premises but are supplemented by cloud compute capacity during periods of high or burst demand.
* **Lift and Shift:** The existing scheduler is moved "as-is" to the cloud, running compute nodes on the cloud with configurations similar to on-premises.
* **AWS Optimized:** The focus is on compute elasticity and using managed services as much as possible, combined with purchasing models (Amazon EC2 Spot, Savings Plans).
* **AWS Native:** Represents a complete reimagining of traditional HPC platforms, emphasizing cloud-native architectures, serverless building blocks, and optimized hardware (AI accelerators).

---

### Workload characteristics for architecture decisions

HPC workloads in FSI have diverse requirements, but some key common characteristics include:

* **Varying Task Duration:** From a few seconds to hours or even days.
* **High Throughput Requirements:** Often need to process tens of thousands of tasks per second.
* **High Parallelization Requirements:** Most calculations are typically loosely coupled, allowing parallel execution.
* **Resource Intensity:** CPU : Memory ratios and I/O requirements.
* **Software Requirements:** Specific operating systems, platforms, and libraries.
* **Data & Application Dependencies:** Local vs. distributed processing.
* **Elasticity & Flexibility:** The ability to scale up and down based on demand.
* **Cost Optimization:** Balancing performance and cost.

We will use the decision tree in Figure 1 to guide the selection of the appropriate platform.

![pic 1](/images/3-Blog/B1-1.png)
> *Figure 1. Decision tree for selecting an HPC solution on the cloud based on workload characteristics.*

Navigation begins with a critical decision: **Keep the existing on-premises scheduler** or **Build a new cloud-native solution**.

#### 1. Migrating your existing scheduler to the cloud

If you choose to keep your existing Grid scheduler due to migration effort concerns or project timelines:

* **Commercial Schedulers:** [IBM Spectrum Symphony](https://www.ibm.com/products/analytics-workload-management) or [TIBCO DataSynapse GridServer®](https://docs.tibco.com/products/tibco-datasynapse-gridserver-manager-7-1-0).
* **Open-source Schedulers:** [Slurm Workload Manager](https://slurm.schedmd.com/documentation.html) or [HTCondor](https://htcondor.org/).

Common migration methods:
* **Hybrid Burst:** Use AWS to supplement the on-premises grid during peaks.
* **Lift-and-Shift:** Move the entire system to AWS "as-is".

#### 2. Building and using a cloud-native HPC scheduler / platform

This approach addresses legacy limitations and maximizes cloud benefits. The decision relies heavily on **Task Duration**:

* **Mixed Short/Long Tasks (Seconds - Minutes):**
    * If familiar with Slurm: Use [AWS ParallelCluster](https://aws.amazon.com/hpc/parallelcluster/) or [AWS Parallel Computing Service](https://aws.amazon.com/pcs/) (managed service).
* **Long Tasks (> 1 minute):**
    * Use [AWS Batch](https://aws.amazon.com/batch/), a fully managed batch computing service (free scheduler, pay only for compute resources).
* **High Throughput (Seconds - Minutes):**
    * Use [HTC-Grid](https://github.com/finos/htc-grid), a community project (FINOS) capable of processing tens of thousands of tasks per second.
* **Very Short Tasks (< 15 minutes):**
    * Leverage serverless architecture with [AWS Lambda](https://aws.amazon.com/lambda/). No "always-on" server management, high throughput, but subject to strict execution time limits.

---

### Conclusion

There is no "one-size-fits-all" solution. The number of tasks and their duration will determine the most suitable solution.

View platform selection as the start of a journey. We often see customers continuing their journey from "Lift & Shift" to "AWS Optimized" and "AWS Native" for continuous optimization.

### Key Takeaways

1.  **If maintaining an existing scheduler:**
    * Commercial solutions (IBM, Tibco) offer stability but may lack cloud flexibility.
    * Open-source solutions (Slurm, HTCondor) can utilize AWS ParallelCluster/PCS for better management.
2.  **If moving to Cloud-native:**
    * **AWS Batch:** For workloads > 5 minutes.
    * **AWS Lambda:** For workloads < 15 minutes.
    * **HTC-Grid:** For high throughput workloads (seconds to minutes).

---

#### About the Authors

> **Mark Norton**
>
> Principal HPC Specialist at AWS with over 30 years of experience. He specializes in designing scalable cloud computing solutions to optimize performance and deliver strategic technological advantages for financial, automotive, and research enterprises.

> **Flamur Gogolli**
>
> Senior Specialist Solutions Architect at AWS. He has extensive experience in infrastructure modernization, from designing complex systems to operating large-scale workloads. Prior to AWS, he led the cloud-native transformation at JP Morgan.