---
title: "Nhật ký Tuần 8"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu Tuần 8

- Nâng cao kiến thức về **kiến trúc hệ thống (Solutions Architecture)** trong môi trường AWS.
- Tìm hiểu và trải nghiệm các **dịch vụ mở rộng khác** của AWS như IoT, Ground Station và RoboMaker.
- Nghiên cứu chuyên sâu các **tài liệu whitepaper, kiến trúc tham chiếu và best practices** chính thức từ AWS.

**Thời gian:** 17/11/2025 - 22/11/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                                                                | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                           |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | -------------------------------------------- |
| 1    | - Tích hợp **Amazon S3 & ElastiCache (Redis)** <br> + Kết nối upload ảnh sản phẩm lên S3 <br> + Cấu hình Redis để cache danh sách sản phẩm, cải thiện hiệu năng truy vấn                                                                      | 17/11/2025   | 17/11/2025    | <https://aws.amazon.com/s3/>               |
| 2    | - Phác thảo **Kiến trúc tổng quan hệ thống** <br> + Tham khảo các kiến trúc mẫu AWS (3-tier, e-commerce) <br> + Xác định danh sách dịch vụ dự kiến dùng: EC2/Elastic Beanstalk, RDS, S3, CloudFront, VPC,…                                   | 18/11/2025   | 18/11/2025    | <https://aws.amazon.com/architecture/>     |
| 3    | - Tối ưu **mô hình dữ liệu & service** của đồ án <br> + Rà soát lại entity, mapping <br> + Điều chỉnh luồng xử lý nghiệp vụ trong Application Layer để phù hợp với triển khai thực tế trên AWS                                                | 19/11/2025   | 19/11/2025    | -                   |
| 4    | - Hoàn thiện nội dung **Báo cáo đề xuất (Proposal)** <br> + Dàn ý: Executive Summary, Problem Statement, Solution Architecture, Implementation Plan, Cost Estimation <br> + Chuẩn bị nội dung chi tiết cho các tuần tiếp theo                 | 19/11/2025   | 19/11/2025    | -                   |
| 5    | - Rà soát kiến trúc và hoàn thiện Proposal <br> + Kiểm tra tương thích giữa các dịch vụ AWS đã chọn <br> + Điều chỉnh mô hình để đảm bảo tính mở rộng, sẵn sàng cao và tối ưu chi phí                       | 20/11/2025   | 20/11/2025    | <https://aws.amazon.com/whitepapers/>        |
| 6    | - Tổng kết Tuần 8 <br> + Tóm tắt kiến thức đã học về kiến trúc, IoT và tài liệu whitepaper <br> + So sánh kiến trúc hybrid, multicloud và serverless <br> + Chuẩn bị nội dung cho **báo cáo tổng kết khóa học AWS Cloud Journey**                                                        | 20/11/2025   | 20/11/2025    | -                                            |

---

### Thành tựu Tuần 8

- Nâng cao hiểu biết về **Advanced Solutions Architecture**:

  - Thiết kế kiến trúc hybrid kết hợp **on-premise** và **AWS Cloud**.
  - Hiểu rõ mô hình **Multi-Cloud** và khi nào nên sử dụng.
  - Áp dụng **Design Patterns** như Microservices, Event-driven và Serverless trong thiết kế hệ thống.

- Làm quen với các **dịch vụ mở rộng của AWS**:

  - Kết nối thiết bị thông minh bằng **AWS IoT Core**.
  - Hiểu quy trình thu nhận và xử lý dữ liệu vệ tinh với **AWS Ground Station**.
  - Tìm hiểu về mô phỏng robot tự động bằng **AWS RoboMaker**.

- Đọc và nghiên cứu **AWS Whitepapers**:

  - Nắm vững **AWS Well-Architected Framework** và 5 trụ cột chính: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization.
  - Hiểu rõ các chiến lược thiết kế **High Availability** và **Disaster Recovery**.
  - Ghi chú các **Best Practices** về bảo mật, tối ưu chi phí và mở rộng hệ thống.

- Tổng hợp kiến thức tuần 8:
  - Kết hợp giữa lý thuyết kiến trúc và thực hành qua các dịch vụ thực tế.
  - Chuẩn bị cho **báo cáo tổng kết và trình bày kiến trúc hệ thống hoàn chỉnh** vào tuần tiếp theo.
