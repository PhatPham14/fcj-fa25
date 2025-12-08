---
title: "Nhật ký Tuần 3"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu Tuần 3

- Hiểu các khái niệm cốt lõi về **High Availability (Tính sẵn sàng cao)** và **Scalability (Khả năng mở rộng)** trong môi trường đám mây.
- Tìm hiểu các dịch vụ cơ sở dữ liệu được quản lý của AWS như **RDS**, **Aurora**, và **ElastiCache**.
- Học cách cấu hình và quản lý **Amazon Route 53** cho DNS và điều hướng truy cập.
- Nghiên cứu các mô hình **kiến trúc giải pháp điển hình trên AWS** và thực hành thiết kế hệ thống tối ưu.

**Thời gian:** 13/10/2025 - 19/10/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                                         | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                     |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | -------------------------------------- |
| 1    | - Nghiên cứu về **High Availability & Scalability** <br> + Tìm hiểu mô hình triển khai **Multi-AZ** <br> + Cấu hình thử nghiệm **Auto Scaling Group** <br> + Hiểu vai trò của **Elastic Load Balancer (ELB)** trong việc phân phối lưu lượng                      | 13/10/2025   | 13/10/2025    | <https://000010.awsstudygroup.com/>    |
| 2    | - Tìm hiểu **Amazon RDS** và **Aurora** <br> + Tạo instance RDS ở chế độ **Multi-AZ** <br> + Thử nghiệm **read replica** và **failover** <br> + Học về cơ chế **Aurora cluster** và khả năng tự phục hồi                                                          | 14/10/2025   | 14/10/2025    | <https://000010.awsstudygroup.com/>    |
| 3    | - Làm việc với **Amazon ElastiCache** <br> + So sánh hai engine **Redis** và **Memcached** <br> + Thực hành tạo cache cluster <br> + Giám sát hiệu suất qua **CloudWatch**                                                                                        | 15/10/2025   | 15/10/2025    | <https://000019.awsstudygroup.com/>    |
| 4    | - Thực hành cấu hình **Amazon Route 53** <br> + Tạo **hosted zone** và bản ghi DNS <br> + Thiết lập **failover routing** <br> + Kiểm tra **latency-based routing** giữa các vùng                                                                                  | 16/10/2025   | 16/10/2025    | <https://aws.amazon.com/route53/>      |
| 5–6  | - Tìm hiểu về **Classic Solutions Architecture** <br> + Phân tích mô hình **multi-tier** và **serverless** <br> + Nghiên cứu các pattern thiết kế có tính mở rộng cao và sẵn sàng trong sản xuất <br> + Thiết kế mô hình nhỏ kết hợp **EC2**, **RDS**, và **ELB** | 17/10/2025   | 19/10/2025    | <https://aws.amazon.com/architecture/> |

---

### Thành tựu Tuần 3

- Nắm vững các chiến lược về **High Availability**:

  - Hiểu cách triển khai **Multi-AZ** và cơ chế **failover tự động**.
  - Cấu hình **Auto Scaling Group** để tự động mở rộng hoặc thu hẹp tài nguyên.
  - Sử dụng **Elastic Load Balancer (ELB)** để đảm bảo phân phối lưu lượng và duy trì thời gian hoạt động liên tục.

- Mở rộng kiến thức về **các dịch vụ cơ sở dữ liệu của AWS**:

  - Quản lý **RDS** và hiểu lợi ích hiệu năng của **Aurora**.
  - Biết cách sử dụng **ElastiCache** để tăng tốc độ phản hồi ứng dụng bằng bộ nhớ đệm.

- Làm chủ các khái niệm về **DNS và định tuyến** thông qua **Amazon Route 53**:

  - Tạo và cấu hình **hosted zone**, **routing policy**, và **health check**.
  - Thực hành **failover routing** và **latency-based routing** giữa các khu vực.

- Tăng cường tư duy thiết kế kiến trúc hệ thống qua **Classic AWS Solutions**:

  - Biết cách kết hợp các dịch vụ **Compute**, **Database**, và **Networking** để xây dựng hệ thống linh hoạt.
  - Thiết kế mô hình thử nghiệm nhỏ tập trung vào tính **ổn định**, **khả năng mở rộng**, và **tối ưu chi phí**.

- Tổng hợp kiến thức đa lĩnh vực về **Compute**, **Database**, **Networking**, và **Architecture Design**, sẵn sàng cho các module chuyên sâu tiếp theo của AWS.
