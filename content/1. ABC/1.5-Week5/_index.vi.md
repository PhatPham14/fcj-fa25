---
title: "Nhật ký Tuần 5"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu Tuần 5

- Học cách triển khai và quản lý **container trên AWS** bằng **ECS**, **EKS**, và **Docker**.
- Hiểu các khái niệm và lợi ích của **kiến trúc Serverless**.
- Thiết kế và xây dựng **ứng dụng Serverless** tích hợp **Lambda**, **API Gateway**, **S3**, và **DynamoDB**.
- Tìm hiểu các dịch vụ **cơ sở dữ liệu AWS** như **RDS**, **Aurora**, **DynamoDB**, **Redshift**, và **ElastiCache**.

**Thời gian:** 27/10/2025 - 02/11/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                               | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                   |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | ------------------------------------ |
| 1    | - Tìm hiểu về **Containers on AWS** <br> + Phân biệt giữa **ECS** và **EKS** <br> + Triển khai container mẫu bằng **ECS (Fargate)** <br> + Làm quen với khái niệm **container orchestration**                                                           | 27/10/2025   | 27/10/2025    | <https://aws.amazon.com/containers/> |
| 2    | - Thực hành với **EKS (Elastic Kubernetes Service)** <br> + Tạo cụm EKS và triển khai ứng dụng mẫu <br> + Kết nối **Docker image** từ local lên **ECR (Elastic Container Registry)** <br> + Theo dõi cụm EKS qua **AWS Console**                        | 28/10/2025   | 28/10/2025    | <https://aws.amazon.com/eks/>        |
| 3    | - Khám phá **Serverless Overview** <br> + Hiểu khái niệm **event-driven computing** <br> + Tạo và kiểm thử **AWS Lambda** cơ bản <br> + Tích hợp **Lambda** với **API Gateway** để tạo endpoint                                                         | 29/10/2025   | 29/10/2025    | <https://aws.amazon.com/lambda/>     |
| 4    | - Thiết kế **Serverless Architecture** <br> + Kết nối **Lambda** với **DynamoDB** và **S3** <br> + Xây dựng pipeline dữ liệu đơn giản bằng **Step Functions** <br> + Kiểm thử quy trình serverless end-to-end                                           | 30/10/2025   | 30/10/2025    | <https://000025.awsstudygroup.com/>  |
| 5    | - Tìm hiểu về **Databases in AWS** <br> + So sánh giữa cơ sở dữ liệu quan hệ và NoSQL <br> + Tạo cơ sở dữ liệu thử nghiệm trong **RDS** và **DynamoDB** <br> + Làm quen với **Redshift** cho phân tích dữ liệu và **ElastiCache** để tăng tốc truy xuất | 31/10/2025   | 31/10/2025    | <https://000025.awsstudygroup.com/>  |
| 6    | - Ôn tập toàn bộ kiến thức trong tuần <br> + Triển khai dự án nhỏ kết hợp **Lambda**, **API Gateway**, **DynamoDB**, và **S3** <br> + Ghi chú lại bài học và các kinh nghiệm tối ưu                                                                     | 1/11/2025    | 1/11/2025     | -                                    |

---

### Thành tựu Tuần 5

- Hiểu rõ và thực hành với **Containers trên AWS**:

  - Triển khai container bằng **ECS (Fargate)** và **EKS**.
  - Nắm vững cách quản lý image với **ECR** và nguyên tắc **container orchestration**.

- Nắm bắt kiến thức nền tảng về **kiến trúc Serverless**:

  - Xây dựng và chạy các hàm **AWS Lambda** theo hướng sự kiện (event-driven).
  - Tích hợp **Lambda** với **API Gateway** để tạo các endpoint RESTful.

- Thiết kế và triển khai thành công **ứng dụng Serverless hoàn chỉnh**:

  - Kết nối **Lambda** với **DynamoDB** và **S3** để xử lý dữ liệu tự động.
  - Sử dụng **Step Functions** để điều phối quy trình làm việc.

- Củng cố kiến thức về **các dịch vụ cơ sở dữ liệu của AWS**:

  - Làm việc với **RDS** cho hệ quản trị quan hệ và **DynamoDB** cho NoSQL.
  - Tìm hiểu **Aurora** về khả năng mở rộng và **Redshift** cho phân tích dữ liệu.
  - Sử dụng **ElastiCache** để tăng hiệu năng truy xuất dữ liệu.

- Áp dụng tư duy **DevOps** trong quá trình triển khai:

  - Kết hợp giữa **Containers**, **Serverless**, và **Databases** trong cùng môi trường triển khai.
  - Hiểu được quy trình phát triển liền mạch giữa các dịch vụ AWS.

- Hoàn thiện kiến thức về **Compute, Database, và Serverless**, sẵn sàng cho **Tuần 6** với chủ đề **Monitoring, CI/CD và Infrastructure as Code (IaC)**.
