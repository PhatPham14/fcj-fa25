---
title: "Nhật ký Tuần 7"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7

- Hiểu và áp dụng các phương pháp **bảo mật dữ liệu và hệ thống** trong AWS.
- Quản lý, cấu hình và tối ưu **Amazon VPC (Virtual Private Cloud)** cho hệ thống mạng riêng.
- Học cách **sao lưu, phục hồi và triển khai kế hoạch khôi phục thảm họa (Disaster Recovery)** với các công cụ AWS.

**Thời gian:** 10/11/2025 - 16/11/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                                                                     | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                 |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | ---------------------------------- |
| 1    | - Bắt đầu viết **Proposal** của đồ án <br> + Hoàn thiện **Executive Summary**, **Problem Statement**, **Kiến trúc tổng quan hệ thống** <br> + Nghiên cứu các dịch vụ AWS sẽ tích hợp trong giai đoạn triển khai sau                                                            | 10/11/2025   | 10/11/2025    | -                   |
| 2    | - Xây dựng **Domain → Persistence → Application Layer** cho Mini-Market <br> + Tạo entity <br> + Thiết lập **Repository & Unit of Work Pattern** <br> + Chạy migration & seed dữ liệu <br> + Triển khai các service xử lý nghiệp vụ chính                                    | 11/11/2025   | 11/11/2025    | -                   |
| 3    | - Khởi tạo **WebShop MVC** <br> + Tạo layout cơ bản (Header, Footer, Navigation) <br> + Xây dựng trang **Danh sách sản phẩm – Giỏ hàng** <br> + Viết phần **Architecture & Technical Implementation** cho Proposal                                                              | 12/11/2025   | 12/11/2025    | -                   |
| 4    | - Vẽ sơ đồ **AWS Architecture Diagram** cho hệ thống <br> + Thu thập thông tin từng dịch vụ sử dụng: <br> &emsp; · Elastic Beanstalk <br> &emsp; · RDS SQL Server <br> &emsp; · Amazon S3 <br> &emsp; · CloudFront <br> &emsp; · WAF & Route 53 <br> &emsp; · ElastiCache Redis <br> &emsp; · NAT Gateway <br> &emsp; · CodePipeline/CodeBuild | 13/11/2025   | 13/11/2025    | -                   |
| 5    | - Tìm hiểu về **Disaster Recovery & Backup** <br> + Sử dụng **AWS Backup** để sao lưu tài nguyên tự động <br> + Cấu hình **RDS Read Replicas** để tăng khả năng chịu lỗi <br> + Thực hành **Cross-Region Failover** cho kế hoạch DR                                                           | 14/11/2025   | 14/11/2025    | <https://aws.amazon.com/backup/>   |
| 6    | - Tổng hợp tiến độ đồ án và cập nhật Proposal <br> + Rà soát kiến trúc, phân quyền, các dịch vụ AWS đã chọn <br> + Chuẩn bị nội dung cho tuần 8: Triển khai S3 upload, cache Redis và tối ưu kiến trúc                                                                    | 15/11/2025   | 15/11/2025    | -                                  |

---

### Thành tựu Tuần 7

- Nắm vững **bảo mật dữ liệu và mã hóa trong AWS**:

  - Thực hành tạo và quản lý **KMS keys** để bảo vệ dữ liệu.
  - Hiểu cơ chế hoạt động của **CloudHSM** trong quản lý khóa phần cứng.
  - Cấu hình **AWS Shield** và **WAF** để bảo vệ ứng dụng khỏi tấn công DDoS và truy cập độc hại.

- Làm chủ **mạng riêng ảo Amazon VPC**:

  - Tạo và cấu hình **VPC**, **subnets**, **route tables**, **Internet Gateway**, và **NAT Gateway**.
  - Áp dụng **Security Groups** và **Network ACLs** để kiểm soát truy cập hiệu quả.
  - Thiết lập **VPN Connection** và hiểu khái niệm **Direct Connect** cho kết nối bảo mật cao.

- Hiểu rõ quy trình **Disaster Recovery (DR)** và sao lưu dữ liệu:

  - Sử dụng **AWS Backup** để quản lý sao lưu định kỳ.
  - Cấu hình **RDS Read Replicas** để đảm bảo tính sẵn sàng dữ liệu.
  - Thực hiện **Cross-Region Failover** để đảm bảo khôi phục nhanh sau thảm họa.

- Tăng cường khả năng thiết kế hệ thống an toàn, đáng tin cậy và có khả năng phục hồi cao.
  - Biết cách kết hợp giữa **Security**, **Networking**, và **Resilience** trong kiến trúc AWS.
  - Chuẩn bị kiến thức cho tuần tiếp theo về **Automation, Infrastructure as Code (IaC), và DevOps Practices**.
