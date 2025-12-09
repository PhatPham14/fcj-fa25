---
title: "AWS IoT Greengrass Nucleus Lite - Revolutionizing Edge Computing on Resource-Constrained Devices"
date: 2025-04-15
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
tags:
  - AWS IoT
  - AWS IoT Greengrass V2
  - Edge Computing
  - IoT Edge
---

**By Camilla Panni and Greg Breen**

[AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html) is an open-source edge runtime and cloud service that helps you build, deploy, and manage multi-process applications at scale across fleets of IoT devices.

AWS IoT Greengrass V2 was launched in December 2020 with a Java-based edge runtime called [nucleus](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-nucleus-component.html). With [release 2.14.0](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-release-2024-12-16.html) in December 2024, AWS introduced an additional edge runtime option: **Nucleus Lite** - written in C.

**AWS IoT Greengrass Nucleus Lite** is a lightweight, [open-source](https://github.com/aws-greengrass/aws-greengrass-lite) edge runtime designed for resource-constrained devices. It extends AWS IoT Greengrass capabilities to lower-cost devices and single-board computers serving applications such as smart home hubs, smart energy meters, smart vehicles, edge AI, and robotics.

This article explains the advantages of both edge runtime options and provides guidance to help you choose the right approach for your use case.

---

### Key differences between Nucleus and Nucleus Lite

AWS IoT Greengrass Nucleus Lite is fully compatible with the AWS IoT Greengrass [V2 Cloud Service API](https://docs.aws.amazon.com/greengrass/v2/APIReference/API_Operations.html) and [IPC](https://docs.aws.amazon.com/greengrass/v2/developerguide/interprocess-communication.html) interface. This means you can build and deploy components targeting one or both runtimes. However, Nucleus Lite has distinct technical characteristics:

#### 1. Memory footprint

* **Nucleus (Java):** Requires a minimum of 256 MB disk and 96 MB RAM. AWS recommends a minimum of **512 MB RAM** to support the OS, JVM, and your applications.
* **Nucleus Lite (C):** Requires less than **5 MB RAM and 5 MB storage**, does not depend on a JVM, and only requires the C Standard Library.

![pic 1](/images/3-Blog/B2-1.png)
> *Figure 1: Comparison of Nucleus vs. Nucleus Lite memory footprint.*

This smaller footprint opens up new possibilities for IoT application development on resource-constrained devices.

#### 2. Static memory allocation

Nucleus Lite allocates a fixed amount of memory at startup and keeps it unchanged.
* **Benefit:** Deterministic resource requirements, minimizing the risk of memory leaks.
* **Performance:** Eliminates non-deterministic latency often found in garbage-collected languages like Java.

#### 3. Directory structure

Nucleus Lite clearly separates components on disk, offering optimized support for **Embedded Linux**:

* **Runtime:** Can be stored on a **Read-Only** partition (supporting A/B OS update mechanisms).
* **Components & Config:** Located on a **Read-Write** partition or overlay for management via deployments.
* **Logs:** Stored in a temporary partition or separate volume to prevent flash memory wear.

This separation helps you create [golden images for mass device manufacturing](https://docs.aws.amazon.com/prescriptive-guidance/latest/iot-greengrass-golden-images/introduction.html).

#### 4. Systemd Integration

[Systemd](https://systemd.io/) is a mandatory requirement for Nucleus Lite.
* Nucleus Lite is installed as a set of systemd services.
* Each deployed component also runs as a separate systemd service.
* Logging is handled centrally by systemd, allowing the use of standard Linux tools for debugging.

---

### Choosing between Nucleus and Nucleus Lite

The choice depends on your specific use case, hardware constraints, and operating system. The table below summarizes the recommendations:

| When to use Nucleus (Java) | When to use Nucleus Lite (C) |
| :--- | :--- |
| You want to use Windows or a Linux distro without systemd | Your device is memory constrained (**≤ 512 MB RAM**) |
| Your application runs in Docker containers | Device CPU clock speed is **< 1 GHz** |
| Application components are Lambda functions | You use Embedded Linux and need strict partition control (OS updates, A/B partitions) |
| You develop using interpreted or scripting languages | You program using compiled languages |
| You need features [not yet supported by Nucleus Lite](https://docs.aws.amazon.com/greengrass/v2/developerguide/operating-system-feature-support-matrix.html) | You have compliance requirements that disallow Java usage |
| You are creating an [AWS IoT SiteWise gateway](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/gw-self-host-gg2.html) | You prioritize static memory allocation |

> *Table 1: Guidance for choosing between Nucleus and Nucleus Lite.*

---

### Use Cases and Deployment Scenarios

#### 1. Use Cases
With low resource requirements, Nucleus Lite is suitable for low-cost devices with limited memory and CPU in sectors such as smart homes, industrial, automotive, and smart metering.

#### 2. Embedded Systems
Nucleus Lite supports Embedded Linux out-of-the-box via the [meta-aws](https://github.com/aws4embeddedlinux/meta-aws) project. This project provides "recipes" for integration into Yocto/OpenEmbedded, and the [meta-aws-demos](https://github.com/aws4embeddedlinux/meta-aws-demos) repository contains examples such as A/B updates using RAUC.

#### 3. Multi-tenancy with containerized Nucleus Lite
With its small footprint, Nucleus Lite enables efficient containerization for multi-tenant models.

![pic 1](/images/3-Blog/B2-2.png)

> *Figure 2: Multi-tenant containerization.*

* **Secure Isolation:** Each container instance maintains strict boundaries.
* **Resource Optimization:** Small footprint allows multiple containers to operate on limited devices.
* **Independent Operation:** Applications are managed and updated separately.

---

### Best Practices

**1. Plugin compatibility:**
Nucleus plugins (written in Java for the original runtime) **cannot** be used with the Nucleus Lite runtime.

**2. Component Language Selection:**
* Choosing Python/Java will reduce the memory-saving advantages of Nucleus Lite (due to the need for an interpreter or JVM).
* **Recommendation:** Rewrite critical components in **C, C++, or Rust** to achieve maximum performance.

**3. Migration and Development:**
* When migrating: You can run existing components "as-is" to ensure functionality before optimizing.
* When calculating memory budgets: Account for all runtime dependencies and system footprint, not just Nucleus Lite itself.

---

### Future and Conclusion

AWS IoT Greengrass Nucleus Lite helps reimagine edge computing deployments by significantly reducing resource requirements. This allows you to:
* Deploy IoT on cheaper, more diverse hardware.
* Reduce operational costs.
* Enable new use cases that were previously unfeasible.

Ready to get started?
* **Explore:** [AWS IoT Greengrass Documentation](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html).
* **Get hands-on:** [Installation Guide](https://github.com/aws-greengrass/aws-greengrass-lite/blob/main/docs/SETUP.md#setting-up-greengrass-nucleus-lite).
* **Community:** Join the [AWS IoT Community Forum](https://repost.aws/topics/TAEQXJMLWWTp2elx_Bkb1Kvw/internet-of-things-iot).
* **Contribute:** Submit code to the [Github repository](https://github.com/aws-greengrass/aws-greengrass-lite).

---

#### About the Authors

> **Camilla Panni**
>
> Solutions Architect at AWS. She supports Public Sector customers in Italy to accelerate cloud adoption. Camilla has a technical background in automation and IoT.

> **Greg Breen**
>
> Senior IoT Specialist Solutions Architect at AWS, based in Australia. With deep experience in embedded systems, Greg supports product development teams across the Asia-Pacific region in bringing devices to market.