---
title: "Nhật ký Tuần 4"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu Tuần 4

- Hiểu và tối ưu hóa **lưu trữ dữ liệu trên Amazon S3**.
- Nâng cao kỹ năng quản lý, bảo mật, và tối ưu hiệu suất **S3**.
- Tìm hiểu về **CloudFront**, **Global Accelerator**, và các phương pháp giảm độ trễ khi phân phối nội dung.
- Nghiên cứu các dịch vụ lưu trữ khác của AWS như **FSx**, **Storage Gateway**, và tích hợp hệ thống qua **SQS**, **SNS**, **Step Functions**.

**Thời gian:** 20/10/2025 - 26/10/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                                | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                            |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | --------------------------------------------- |
| 1    | - Tìm hiểu **Amazon S3 cơ bản** <br> + Tạo bucket và upload dữ liệu mẫu <br> + So sánh các loại **storage tiers** (Standard, Infrequent Access, Glacier) <br> + Phân tích chi phí lưu trữ theo từng lớp dữ liệu                                          | 29/09/2025   | 29/09/2025    | <https://000024.awsstudygroup.com/>           |
| 2    | - Nâng cao quản lý **Amazon S3** <br> + Cấu hình **Cross-Region Replication (CRR)** giữa hai vùng khác nhau <br> + Thiết lập **Lifecycle Policy** để tự động chuyển dữ liệu sang Glacier <br> + Bật **Versioning** và kiểm tra khả năng phục hồi dữ liệu | 30/09/2025   | 30/09/2025    | <https://000024.awsstudygroup.com/>           |
| 3    | - Thực hành **bảo mật dữ liệu S3** <br> + Áp dụng **IAM policy** và **bucket policy** hạn chế truy cập <br> + Cấu hình **Server-Side Encryption (SSE)** và **AWS KMS** <br> + Kiểm tra thiết lập ngăn chặn truy cập công khai (Block Public Access)      | 01/10/2025   | 01/10/2025    | <https://000057.awsstudygroup.com/>           |
| 4    | - Khám phá **CloudFront & Global Accelerator** <br> + Cấu hình **CloudFront Distribution** để phân phối nội dung từ S3 <br> + Kết hợp **Global Accelerator** để giảm độ trễ truy cập toàn cầu <br> + Đánh giá hiệu suất qua công cụ đo tốc độ truy cập   | 02/10/2025   | 02/10/2025    | <https://000057.awsstudygroup.com/>           |
| 5    | - Tìm hiểu **AWS Storage Extras** <br> + Làm quen với **AWS Storage Gateway** và cơ chế hybrid storage <br> + Cấu hình thử nghiệm **FSx for Windows** và **FSx for Lustre** <br> + So sánh hiệu năng giữa các giải pháp lưu trữ                          | 03/10/2025   | 03/10/2025    | <https://www.youtube.com/watch?v=_yunukwcAwc> |
| 6    | - Nghiên cứu **AWS Integration & Messaging** <br> + Học cách sử dụng **SQS** cho message queue <br> + Gửi và nhận thông báo qua **SNS** <br> + Thiết lập **AWS Step Functions** để điều phối workflow giữa các dịch vụ                                   | 04/10/2025   | 04/10/2025    | <https://000013.awsstudygroup.com/>           |

---

### Thành tựu Tuần 4

- Hiểu rõ cách hoạt động của **Amazon S3** và phân loại **các lớp lưu trữ dữ liệu**:

  - Biết cách lựa chọn **storage class** phù hợp với từng nhu cầu sử dụng.
  - Nắm rõ chi phí, hiệu suất và độ bền (durability) của từng lớp dữ liệu.

- Thực hành nâng cao trong **quản lý S3**:

  - Thiết lập thành công **Cross-Region Replication** giữa hai vùng AWS.
  - Áp dụng **Lifecycle Policy** để tối ưu chi phí lưu trữ dài hạn.
  - Bật **Versioning** và khôi phục dữ liệu bị xóa hoặc ghi đè.

- Củng cố kỹ năng **bảo mật dữ liệu S3**:

  - Áp dụng chính sách **IAM**, **Bucket Policy**, và mã hóa **SSE, KMS**.
  - Đảm bảo bucket không công khai, tuân thủ nguyên tắc bảo mật AWS.

- Làm quen với **CloudFront** và **Global Accelerator**:

  - Thiết lập phân phối nội dung toàn cầu và kiểm tra độ trễ.
  - Hiểu cách CDN và accelerator cải thiện trải nghiệm người dùng.

- Khám phá các **dịch vụ lưu trữ mở rộng của AWS**:

  - Làm quen với **Storage Gateway** cho môi trường hybrid.
  - Tìm hiểu **FSx for Windows File Server** và **FSx for Lustre** cho workload hiệu năng cao.

- Hiểu cơ chế **Integration & Messaging trên AWS**:

  - Sử dụng **SQS** để tách hàng đợi xử lý.
  - Gửi thông báo qua **SNS** và điều phối workflow với **Step Functions**.

- Tổng hợp kiến thức toàn diện về **Storage, Security, Networking, và Integration**, chuẩn bị cho giai đoạn học về **Serverless & Application Deployment** trong những tuần tiếp theo.
