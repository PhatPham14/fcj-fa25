---
title: "Event 4: AWS Well-Architected Security Pillar Workshop"
date: 2025-11-29
weight: 2
chapter: false
pre: " <b> 4.4. </b> "
---

# Summary Report: “AWS Well-Architected Security Pillar Workshop”

### Thông tin sự kiện

- **Thời gian:** 08:30 – 12:00, Thứ Bảy, ngày 29/11/2025 (Morning Only).
- **Địa điểm:** Văn phòng AWS Vietnam, Tòa nhà Bitexco Financial Tower, Quận 1, TP.HCM.
- **Chủ đề:** Bảo mật đám mây toàn diện dựa trên khung kiến trúc AWS Well-Architected.

### Mục tiêu tham dự

- **Củng cố tư duy bảo mật:** Hiểu sâu về 5 trụ cột bảo mật (Identity, Detection, Infrastructure, Data, Incident Response).
- **Áp dụng thực tế:** Học cách thiết kế hệ thống tuân thủ nguyên tắc "Zero Trust" và "Defense in Depth" (Phòng thủ theo chiều sâu).
- **Chuẩn bị cho tương lai:** Nắm bắt roadmap cho các chứng chỉ bảo mật nâng cao (AWS Security Specialty).

### Nội dung chính & Agenda

Buổi workshop tập trung cao độ vào các thực hành bảo mật tốt nhất (Best Practices), chia thành các phiên chuyên sâu:

#### 1. Security Foundation (08:30 – 08:50)
- **Nguyên tắc cốt lõi:** Least Privilege (Quyền tối thiểu), Zero Trust (Không tin tưởng mặc định), và Defense in Depth.
- **Mô hình trách nhiệm chia sẻ (Shared Responsibility Model):** Hiểu rõ ranh giới trách nhiệm giữa AWS và khách hàng.
- **Thực trạng:** Top các mối đe dọa bảo mật phổ biến tại môi trường doanh nghiệp Việt Nam.

#### 2. Năm trụ cột bảo mật (08:50 – 11:40)
* **Pillar 1 - Identity & Access Management (IAM):**
    * Chuyển đổi từ IAM Users sang **IAM Identity Center** (SSO).
    * Sử dụng SCP và Permission Boundaries để quản lý môi trường đa tài khoản (Multi-account).
    * **Demo:** Mô phỏng truy cập và validate IAM Policy.
* **Pillar 2 - Detection:**
    * Giám sát liên tục với **GuardDuty** và **Security Hub**.
    * Tự động hóa cảnh báo (Alerting) sử dụng EventBridge.
* **Pillar 3 - Infrastructure Protection:**
    * Bảo vệ mạng lưới với WAF, Shield và Network Firewall.
    * Phân vùng VPC (Segmentation) và mô hình Security Groups vs NACLs.
* **Pillar 4 - Data Protection:**
    * Quản lý khóa mã hóa với **KMS** (Key rotation, policies).
    * Bảo vệ dữ liệu nhạy cảm bằng **Secrets Manager**.
* **Pillar 5 - Incident Response (IR):**
    * Vòng đời phản ứng sự cố.
    * Xây dựng Playbook cho các kịch bản: lộ IAM key, S3 public exposure, EC2 malware.

### Điểm nhấn & Bài học (Key Takeaways)

#### Identity là bức tường lửa mới
- Trước đây em thường tập trung vào Firewall mạng, nhưng workshop này nhấn mạnh rằng trong Cloud, **Identity (Định danh)** mới là lớp bảo mật quan trọng nhất. Việc quản lý chặt chẽ IAM Roles và Policies là chốt chặn đầu tiên và hiệu quả nhất.

#### Tự động hóa phản ứng sự cố (IR Automation)
- Khái niệm **"Automated Response"** thực sự ấn tượng. Thay vì đợi con người can thiệp khi có sự cố, chúng ta có thể dùng Lambda functions để tự động cô lập (isolate) một EC2 instance bị nhiễm mã độc hoặc thu hồi (revoke) một IAM key bị lộ ngay lập tức.

#### Bảo mật không được làm chậm tốc độ phát triển
- Thông điệp "Security as Code" giúp em hiểu rằng bảo mật nên được tích hợp vào quy trình DevOps (DevSecOps) ngay từ đầu chứ không phải là rào cản ở phút chót.

### Hình ảnh sự kiện

![Không gian lớp học Security](/images/4-Events/security-workshop-1.jpg)
*(Tập trung cao độ tại phiên Security Pillar)*

![Demo Incident Response](/images/4-Events/security-workshop-2.jpg)
*(Mô phỏng quy trình xử lý sự cố bảo mật thực tế)*

![Tổng kết khóa học](/images/4-Events/security-workshop-3.jpg)
*(Chụp ảnh lưu niệm tổng kết chuỗi workshop)*

### Cảm nhận cá nhân

Mặc dù diễn ra vào sáng thứ Bảy sau khi đã hoàn thành Final Showcase, buổi workshop này vẫn thu hút em tham gia đầy đủ vì tầm quan trọng của nó.

Kiến thức về bảo mật thường khô khan, nhưng cách tiếp cận qua các Playbook thực tế (như xử lý khi bị lộ S3 bucket) làm cho bài học trở nên rất dễ hiểu. Đây là hành trang kiến thức vững chắc để em tự tin hơn khi tham gia vào các dự án thực tế tại doanh nghiệp sau kỳ thực tập, nơi bảo mật luôn là ưu tiên hàng đầu.

> **Lời kết:** Một cái kết trọn vẹn cho chuỗi training kỹ thuật, hoàn thiện mảnh ghép cuối cùng của một Cloud Engineer: **Bảo mật**.