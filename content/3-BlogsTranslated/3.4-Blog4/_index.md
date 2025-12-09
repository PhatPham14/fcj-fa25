---
title: "The Frugal HPC Architect – Ensuring Effective FinOps for HPC Workloads at Scale"
date: 2025-04-08
weight: 1
chapter: false
pre: " <b> 3.4. </b> "
tags:
  - HPC
  - FinOps
  - Best Practices
---

**By Alex Kimber**

![pic 1](/images/3-Blog/B3-1.png)

Adopting flexible, on-demand, and scalable computing in the cloud brings many benefits. It frees organizations from long, repetitive procurement processes associated with on-premises infrastructure, which often require educated guesses for sizing, resulting in infrastructure that is only as good as the day it was installed. While the focus of this article is on cost reduction, it is also important to recognize the opportunities that testing at scale can unlock. The cloud allows customers to achieve levels of scale that would be financially impossible with on-premises infrastructure because it can be provisioned for the duration of any individual workload and then released. However, with flexible provisioning in the cloud comes cost variability that can concern organizations with fixed budgets or tight profit margins.

In this article, we will explore best practices we've seen from our work with customers across various industries running HPC workloads at scale. Additionally, we will reference guidance from Werner Vogels, an industry leader who developed ['The Frugal Architect'](https://thefrugalarchitect.com/) to help organizations think about these challenges and find the right balance between the competing requirements of flexibility, efficiency, and system performance.

### HPC and the Cloud

High Performance Computing (HPC) systems are becoming increasingly common on AWS and were among the first workloads to leverage flexible computing at scale, whether supplementing on-premises capacity with 'burst' models or as a primary venue for large-scale computing. Although lessons from The Frugal Architect are broadly applicable, there are some specific lessons that apply to HPC workloads.

HPC includes both tightly coupled systems running workloads such as Computational Fluid Dynamics (CFD), or massive loosely coupled systems that might run financial models. Both have the potential to generate significant costs for their consumers, so careful consideration of the design, measurement, and observability of these systems is all the more important. This article will focus on opportunities for loosely coupled workloads, but many of these will apply to any HPC workload.

### Cost and Frugal Tools

The first 'Law' of The Frugal Architect is **“Make Cost a Non-Functional Requirement”**, emphasizing the importance of considering cost alongside other requirements such as security, accessibility, compliance, and maintainability as measures of a system's success.

In a 'pay as you go' provisioning model, cost is the product of unit cost and the number of units consumed. Optimization can come from reducing the cost of a given unit, consuming fewer units – or both. You can achieve this in various ways for HPC systems running on the cloud, and AWS has services and features to support each method.

#### Reducing Unit Cost

AWS offers many opportunities to reduce unit costs when using its services. Each strategy has trade-offs that may or may not affect application performance, but once evaluated and deployed, can yield significant benefits.

One high-impact example of reducing compute unit costs is [Amazon EC2 Spot](https://aws.amazon.com/ec2/spot/), which allows customers to save up to 90% compared to on-demand provisioning for the same compute capacity. The trade-off with EC2 Spot is that these instances come from pools ready to serve on-demand consumers, and thus they can be reclaimed by AWS at any time with a 2-minute warning. HPC workloads that can tolerate intermittent interruptions (either because individual tasks are short or because they can checkpoint their progress) can realize significant savings with EC2 Spot with minimal disruption.

There are also commercial offerings for customers with a steady level of demand. In this scenario, [Amazon EC2 Savings Plan](https://aws.amazon.com/savingsplans/compute-pricing/) allows customers to save up to 72% in exchange for committing to that capacity for 1 or 3 years. Typically, customers will combine EC2 Spot, Savings Plans, and on-demand capacity to achieve an optimal mix.

Beyond commercial solutions, there are technical opportunities to reduce unit compute costs by ensuring you only provision what you need. AWS currently offers over 750 EC2 instance types, so customers can find the right instance type for their workload. This represents a shift from traditional on-premises provisioning, where homogeneous deployments are used to support the broadest possible set of tasks. On the cloud, each workload can provision the right mix of CPU, GPU, memory, storage, and network performance, avoiding paying for unused capabilities and features.

Beyond compute instances, AWS offers a range of data storage services that present opportunities to reduce unit storage costs. For example, depending on the characteristics of a given workload, it may be optimal to use [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) – possibly with [Mountpoint](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mountpoint.html) if you need POSIX access – instead of a traditional network file system. From there, you can explore services like [Amazon S3 Intelligent-Tiering](https://aws.amazon.com/s3/storage-classes/intelligent-tiering/) to further reduce unit costs per GB of storage if there are infrequently accessed files.

For every application, there may be several opportunities to reduce the unit cost of resources on AWS. By analyzing potential benefits and trade-offs, you can prioritize options and explore those with the most potential benefit for any individual workload, avoiding a 'one size fits all' approach.

#### Reducing Unit Consumption

Consumed units will vary depending on the AWS service you are using. Some services even have multiple unit types, covering different usage patterns (e.g., Amazon S3 has consumption units for GET operations as well as for GB of data stored).

There are several effective ways to reduce Amazon EC2 core-hour unit consumption; for example, you can increase efficiency by ensuring that – as much as possible – cores are performing compute tasks and not idling or working on non-compute activities. Or you can monitor effectiveness by ensuring the value of the work in progress exceeds the cost of the provisioned compute resources; otherwise, consider not running that workload. This aligns with the second law of The Frugal Architect – **“Systems that Last Align Cost to Business”**, ensuring that any cost increase is understood in the context of revenue.

The focus on efficiency and effectiveness represents a significant difference from on-premises task scheduling, where capacity is static. In that scenario, low-value or inefficient workloads might be acceptable because they incur no additional cost and can be run at low priority. While this is also true on the cloud when capacity is covered by a Savings Plan, any additional capacity provisioned incurs additional cost that needs to be evaluated against revenue value.

One group of methods to reduce compute unit consumption is to analyze the billing lifecycle of an AWS instance, from the moment the operating system (OS) starts booting until termination. This time can include overhead activities such as: OS boot, downloading and installing binaries, launching HPC client agents, connecting to the scheduler, idle time with no tasks, or tasks waiting for dependent data. By minimizing time spent on overhead and maximizing time spent on useful computation, you can improve system efficiency, reducing the number of compute units needed for a given workload.

Total OS boot time costs can be reduced by: optimizing individual boot processes, reducing the number of instance boots by using long-running On-Demand Instances, or diversifying instance selection to minimize EC2 Spot Interruption events requiring replacement instance launches. CPU cores waiting for data can be kept busy by a level of task oversubscription, for example running 10 threads on a system with 8 vCPUs.

Arm-based AWS Graviton instances can deliver significant price/performance benefits compared to x86 instances running HPC workloads. Graviton instances provide up to 40% better price performance while using up to 60% less energy than comparable EC2 instances. Since AWS Graviton processors execute the Arm64 instruction set, you may need to take some steps to port applications, but AWS provides the [AWS Porting Advisor for Graviton](https://github.com/aws/porting-advisor-for-graviton) to assist with this. You can track the impact of Graviton adoption using the [AWS Graviton Savings Dashboard](https://aws.amazon.com/ec2/graviton/graviton-savings-dashboard/). Performance benefits from Graviton can help you complete workloads faster for the same cost, or reduce cost by provisioning fewer instances for the same duration.

A good metric to evaluate success in reducing unit consumption is CPU utilization. If your Amazon EC2 instances have periods of significantly low utilization, you might simply need to use fewer instances, but run them at higher utilization.

HPC applications using large data can also benefit from opportunities to reduce high-performance storage consumption. For example, many HPC workloads on the cloud use the [Amazon FSx for Lustre](https://aws.amazon.com/fsx/lustre/) filesystem, providing throughput of hundreds of GB/s and millions of IOPS. But storing the entire dataset on Lustre might not be justifiable. Typically, customers [link the filesystem with Amazon S3](https://docs.aws.amazon.com/fsx/latest/LustreGuide/create-dra-linked-data-repo.html). In this way, FSx for Lustre presents Amazon S3 objects as files, which can be imported into Lustre on demand. This significantly reduces the size of the Lustre filesystem while maintaining high performance. Further reductions can be achieved by enabling [Lustre data compression](https://docs.aws.amazon.com/fsx/latest/LustreGuide/data-compression.html), reducing the filesystem capacity needed for a given dataset.

Another method is to use [Amazon File Cache](https://aws.amazon.com/filecache/), providing high-performance access to Amazon S3 object storage while caching files stored in on-premises NFSv3 filesystems, reducing the cost of duplicate data storage on the cloud. Additional savings can be achieved for both Amazon File Cache and FSx for Lustre by turning them off when not in use and recreating them when demand returns.

### Observability

The fourth law of The Frugal Architect is **“Unobserved Systems lead to unknown costs”**. In the previous section, we introduced core concepts of efficiency (ensuring provisioned resources spend the least time on overhead work) and effectiveness (ensuring work value exceeds the cost of provisioned compute resources).

Both are hard to evaluate without observability systems, which help HPC managers know overall efficiency through metrics like computation as a percentage of capacity provisioned, and help customers know effectiveness through measures of business value as a percentage of cost to compute (hopefully over 100%).

By providing these metrics in a timely and granular manner, stakeholders can identify and quantify continuous improvement opportunities, measure the results of changes, and detect unexpected outcomes quickly. AWS provides many tools supporting observability across metrics, logs, and traces, such as [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) or [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/).

It is also important to have clear visibility into cost (and if possible, cost attribution), and have tools to support accessing, analyzing, and understanding cost data. For example, [AWS Data Exports](https://aws.amazon.com/aws-cost-management/aws-data-exports/) allows exporting data in the FinOps Open Cost and Usage Specification ([FOCUS](https://focus.finops.org/)) 1.0 standard, which can be processed by existing reporting solutions or visualized with [Amazon QuickSight](https://aws.amazon.com/quicksight). [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) also allows granular cost exploration, from high-level overviews to deep dives to identify trends, anomalies, or key cost drivers.

Finally, [AWS Compute Optimizer](https://aws.amazon.com/compute-optimizer/) helps identify underutilized resources and recommends how to address them. For example, it might suggest choosing an instance with less memory if the current provision is underused. Recommendations come with potential savings to help you make better decisions.

### Conclusion

When planning migration or expanding HPC workloads to the cloud, cost needs to be considered alongside other non-functional requirements. This article explored the shift in cost drivers when moving systems to the cloud, and how mechanisms applicable to on-premises clusters may no longer be suitable.

HPC systems can benefit greatly from the flexibility and scalability of the AWS Cloud; costs can therefore be significant and need to be clearly understood. Cost generation varies depending on how compute, storage, and other resources are used on the cloud, requiring different cost management than fixed-capacity on-premises infrastructure.

AWS provides many effective mechanisms to maximize the scale and elasticity the cloud offers, while ensuring you can understand and manage costs. With guiding principles like those in The Frugal Architect, AWS tools and frameworks help build efficient, flexible, and robust architectures to support HPC workloads.

Consider the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected), which provides a dedicated pillar on [cost-optimization](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html) alongside other non-functional keys like security, reliability, and sustainability.

---

#### About the Author

> **Alex Kimber**
>
> Alex Kimber is a Principal Solutions Architect at AWS Global Financial Services, with over 20 years of experience building and operating high-performance grid computing platforms at investment banks.