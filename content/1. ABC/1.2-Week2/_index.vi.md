---
title: "Nhật ký Tuần 2"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu Tuần 2

- Tìm hiểu và áp dụng **AWS IAM** để quản lý danh tính và quyền truy cập.
- Thực hành triển khai và quản lý **EC2 Instance**.
- Khám phá **Amazon VPC** và **AWS Site-to-Site VPN** để hiểu các khái niệm mạng cơ bản.
- Củng cố kiến thức nền tảng về **ngôn ngữ lập trình C#**.

**Thời gian:** 06/10/2025 - 12/10/2025

---

### Tổng quan Nhiệm vụ Tuần

| Ngày | Hoạt động                                                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày kết thúc | Tài liệu tham khảo                                 |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | ------------- | -------------------------------------------------- |
| 1    | - Tìm hiểu các khái niệm cơ bản về **IAM** <br> + Học cách tạo và gán **user, group, role** <br> + Thiết lập **permission policy** cho từng nhóm quyền <br> + Kiểm tra truy cập qua IAM Console                                                                                                    | 06/10/2025   | 06/10/2025    | <https://youtu.be/BPuD1l2hEQ4?si=NViLlKYS7Z2v1EmH> |
| 2    | - Thực hành triển khai **EC2 Instance** và cấu hình cơ bản <br> + Chọn **Amazon Linux 2023 (Free Tier)** <br> + Cấu hình **key pair**, **security group** (SSH access) <br> + Kết nối qua SSH và kiểm tra hoạt động <br> + Làm quen với **VPC networking** (subnet, route table, Internet Gateway) | 07/10/2025   | 07/10/2025    | <https://youtu.be/CXU8D3kyxIc>                     |
| 3    | - Khám phá **Amazon Bedrock Playground** <br> + Trải nghiệm các mô hình như _Claude 3 Haiku_ và _Titan Text_ <br> + Tạo prompt mẫu và đánh giá phản hồi <br> + Thử nghiệm nhiều tình huống khác nhau để hiểu cách AI xử lý                                                                         | 08/10/2025   | 08/10/2025    | <https://000003.awsstudygroup.com/>                |
| 4    | - Ôn tập **lập trình C# cơ bản** <br> + Ôn lại cấu trúc điều khiển, vòng lặp, lớp và đối tượng <br> + Thực hành viết code nhỏ minh họa thao tác logic <br> + Tổng hợp thuật ngữ và dịch vụ AWS qua ChatGPT để ghi nhớ                                                                              | 09/10/2025   | 10/10/2025    | -                                                  |

---

### Thành tựu Tuần 2

- Hiểu và áp dụng được các nguyên tắc của **IAM**, bao gồm tạo người dùng, vai trò và chính sách truy cập.

  - Biết cách cấp quyền hạn chế và tạo nhóm quyền phù hợp với từng nhu cầu.
  - Nắm được mối quan hệ giữa **user, group, role** và **policy** trong AWS.

- Thực hành thành công việc triển khai, kết nối và quản lý **EC2 Instance** trong gói Free Tier.

  - Nắm được cách khởi tạo, dừng, xóa instance và quản lý qua **EC2 Console**.
  - Biết cách truy cập SSH và kiểm tra hoạt động của máy ảo.

- Nắm vững kiến thức nền tảng về **Amazon VPC**, bao gồm:

  - **Subnet**, **Route Table**, **Internet Gateway**, **NAT Gateway** và cấu trúc mạng logic.
  - Hiểu cơ chế định tuyến và cách cô lập mạng ảo an toàn.

- Tìm hiểu cơ chế của **AWS Site-to-Site VPN**, giúp kết nối an toàn giữa mạng nội bộ (on-premises) và VPC.

  - Biết cách hoạt động của tunnel VPN và cách thiết lập kết nối giữa hai hệ thống.

- Trải nghiệm **Amazon Bedrock Playground**, làm quen với các mô hình AI như Claude và Titan.

  - Hiểu cách viết prompt hiệu quả để nhận phản hồi chính xác.
  - Thử nghiệm nhiều chủ đề khác nhau để hiểu cơ chế sinh nội dung (generative AI).

- Củng cố kiến thức **lập trình C#**, song song với thực hành các dịch vụ AWS.

  - Viết các chương trình nhỏ phục vụ kiểm tra logic và học cú pháp cơ bản.

- Có cái nhìn tổng quan về các nhóm dịch vụ chính trong AWS:
  - **Compute** (EC2, Lambda), **Networking** (VPC, VPN), và **AI/ML** (Bedrock).
  - Hiểu được cách các dịch vụ này phối hợp để tạo nên một hệ thống cloud hoàn chỉnh.
