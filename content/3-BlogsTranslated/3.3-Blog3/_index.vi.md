---
title: "Các chiến lược chủ động cho cyber resilience và business continuity trên AWS"
date: 2025-07-11
weight: 2
chapter: false
pre: " <b> 3.3. </b> "
tags:
  - AWS Public Sector
  - Best Practices
  - Disaster Response
  - Security
---

**Bởi Devin Gordon và Henrik Balle**

![pic 1](/images/3-Blog/B3-1.png)

[Amazon Web Services (AWS)](https://aws.amazon.com/) khuyến nghị các tổ chức chuẩn bị phục hồi workloads nếu xảy ra các sự cố cybersecurity hoặc các sự kiện business continuity như thiên tai hoặc lỗi kỹ thuật. Trong bài đăng này, chúng tôi đưa ra hướng dẫn và chiến lược cho các tổ chức trong lĩnh vực Public Sector để sử dụng hạ tầng AWS nhằm vận hành các hệ thống resilient trên cloud.

AWS khuyến nghị khách hàng của mình:
* Sử dụng các framework cho cybersecurity và best practices kiến trúc AWS.
* Triển khai môi trường đa tài khoản (multi-account environment).
* Sử dụng [infrastructure as code (IaC)](https://aws.amazon.com/what-is/iac/) để triển khai các môi trường AWS và workloads.
* Chuẩn bị một recovery account tại một Availability Zone hoặc [Region](https://docs.aws.amazon.com/glossary/latest/reference/glos-chap.html#region) khác với workload chính.
* Đưa tất cả mã ứng dụng, mã IaC, files cấu hình và các phụ thuộc khác vào recovery account.
* Định nghĩa chiến lược backup dữ liệu đến account phục hồi.
* Triển khai testing tự động (unit và full workload) trong account phục hồi.

---

### Use an established framework

Khi các sự cố cybersecurity như ransomware ngày càng gia tăng, các tổ chức Public Sector tìm đến các framework như [NIST Cybersecurity Framework (CSF) 2.0](https://www.nist.gov/cyberframework) của [National Institute of Standards and Technology (NIST)](https://www.nist.gov/) để hướng dẫn quản trị rủi ro cybersecurity tốt hơn. Mặc dù CSF sắp xếp các kết quả cybersecurity theo các chức năng (govern, identify, protect, detect, respond, recover), NIST không quy định cách thức cụ thể để đạt được các kết quả đó.

Để có hướng dẫn cụ thể hơn, hãy tham khảo các tài nguyên như:
* **[AWS Blueprint for Ransomware Defense](https://d1.awsstatic.com/whitepapers/compliance/AWS-Blueprint-for-Ransomware-Defense.pdf):** Cung cấp mapping các dịch vụ AWS với các chức năng CSF.
* **[AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/):** Đi sâu qua sáu trụ cột để giúp kiến trúc sư cloud xây dựng hạ tầng secure, high-performing, resilient và efficient, theo mô hình [AWS Shared Responsibility](https://aws.amazon.com/compliance/shared-responsibility-model/).

Các framework này được bổ sung bởi [AWS Security Reference Architecture (AWS SRA)](https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture/welcome.html), giúp bạn thiết kế, triển khai và quản lý các dịch vụ security AWS.

---

### Implement a multi-account strategy on AWS

AWS khuyến nghị tuân theo best practice khi triển khai môi trường đám mây bằng chiến lược đa tài khoản (multi-account strategy), còn được gọi là [landing zone](https://docs.aws.amazon.com/prescriptive-guidance/latest/migration-aws-environment/understanding-landing-zones.html). Sử dụng [AWS Organizations](https://aws.amazon.com/organizations/) cùng với [AWS Control Tower](https://aws.amazon.com/controltower/) hoặc [Landing Zone Accelerator on AWS](https://aws.amazon.com/solutions/implementations/landing-zone-accelerator-on-aws/) tạo ra môi trường phù hợp cho việc quản lý và tự động hóa. Việc này giúp cô lập và quản lý ứng dụng, dữ liệu, và loại bỏ chuyển động ngang không mong muốn (lateral movement).

Trong chiến lược multi-account, AWS khuyến nghị quản lý trung tâm danh tính bằng [AWS IAM Identity Center](https://aws.amazon.com/iam/identity-center/).
> **Lưu ý:** Trong tình huống phục hồi, bạn có thể phải [dùng root credentials](https://docs.aws.amazon.com/managedservices/latest/userguide/how-when-to-use-root.html). Root credentials nên được bảo mật đúng cách để ngăn takeover account. AWS [gần đây công bố](https://aws.amazon.com/blogs/aws/centrally-managing-root-access-for-customers-using-aws-organizations/g-aws-organizations/) các khả năng mới để quản lý root credentials tập trung nhằm củng cố posture bảo mật.

---

### Build your AWS infrastructure with automation

Là một nguyên tắc then chốt của DevSecOps, AWS khuyến nghị triển khai toàn bộ hạ tầng AWS bằng **Infrastructure as Code (IaC)**. IaC giúp lặp nhanh hạ tầng, cải thiện tính nhất quán, giảm lỗi cấu hình, và quan trọng nhất là đóng vai trò như tài liệu cho hạ tầng để tăng tốc phục hồi.

Các công cụ và dịch vụ hỗ trợ:
* **[AWS CloudFormation](https://aws.amazon.com/cloudformation/):** Định nghĩa hạ tầng bằng template. Có thể [tạo stack từ hạ tầng hiện có](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/resource-import-new-stack.html).
* **[AWS Cloud Development Kit (AWS CDK)](https://aws.amazon.com/cdk/):** Định nghĩa resource bằng ngôn ngữ lập trình.
* **[AWS Serverless Application Model (AWS SAM)](https://aws.amazon.com/serverless/sam/):** Framework cho ứng dụng serverless.
* **[HashiCorp Terraform](https://developer.hashicorp.com/terraform):** Công cụ IaC đa nền tảng.

Mã IaC nên được lưu trữ trong source code repository (ví dụ: GitLab). Bạn có thể sử dụng [DevOps Pipeline Accelerator (DPA)](https://github.com/aws-samples/aws-devops-pipeline-accelerator) để xây dựng CI/CD pipeline chuẩn hóa.

---

### Prepare a recovery location

AWS khuyến nghị thiết lập các tài khoản riêng biệt dành cho khôi phục (recovery) để đối phó với sự cố an ninh mạng.

Để đối phó với sự cố kỹ thuật hoặc thiên tai (ví dụ: [AWS Availability Zone](https://docs.aws.amazon.com/global-infrastructure/latest/regions/aws-availability-zones.html) outage):
* Nếu dùng cùng Region, đảm bảo AZ dùng cho khôi phục là riêng biệt so với workload chính.
* Sử dụng **Availability Zone ID (AZ ID)** để đảm bảo tính nhất quán giữa các tài khoản (do AWS ngẫu nhiên hóa tên AZ giữa các tài khoản).

![pic 1](/images/3-Blog/B3-2.png)
> *Hình 1. Ví dụ về workload và recovery account sử dụng Availability Zone ID.*

Để tăng khả năng chịu lỗi cao hơn, hãy cân nhắc **khôi phục đa Region (multi-Region recovery)**. Ví dụ: Region chính ở *US East (N. Virginia)* và backup ở *US East (Ohio)*. Hãy đánh giá chiến lược khóa mã hóa với [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms/) để giải mã dữ liệu backup cross-region.

---

### Xác định chiến lược backup và triển khai kiểm thử tự động

AWS khuyến nghị căn chỉnh chiến lược backup với các giải pháp cloud