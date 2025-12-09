---
title: "Event 3: DevOps on AWS Workshop"
date: 2025-11-17
weight: 2
chapter: false
pre: " <b> 4.3. </b> "
---

# Summary Report: “DevOps on AWS Workshop”

### Thông tin sự kiện

- **Thời gian:** 08:30 – 17:00, Thứ Hai, ngày 17/11/2025.
- **Địa điểm:** Văn phòng AWS Vietnam, Tòa nhà Bitexco Financial Tower, Quận 1, TP.HCM.
- **Chủ đề:** Văn hóa DevOps, Tự động hóa quy trình (CI/CD), Hạ tầng dưới dạng mã (IaC) và Giám sát hệ thống.

### Mục tiêu tham dự

- **Chuẩn hóa quy trình:** Hiểu rõ văn hóa DevOps và các chỉ số đo lường hiệu quả (DORA metrics) để áp dụng vào quy trình làm việc nhóm.
- **Tự động hóa:** Làm chủ bộ công cụ AWS Developer Tools (CodeCommit, CodeBuild, CodeDeploy, CodePipeline) để xây dựng pipeline CI/CD hoàn chỉnh.
- **Quản lý hạ tầng:** Tiếp cận tư duy Infrastructure as Code (IaC) với AWS CDK để quản lý tài nguyên hiệu quả hơn.
- **Vận hành:** Học cách giám sát và truy vết lỗi (Observability) cho ứng dụng Microservices.

### Nội dung chính & Agenda

Workshop kéo dài cả ngày với khối lượng kiến thức chuyên sâu, chia làm hai buổi sáng và chiều:

#### 1. Buổi sáng: DevOps Mindset & CI/CD (08:30 – 12:00)
- **DevOps Culture:** Hiểu rằng DevOps không chỉ là công cụ mà là văn hóa kết hợp giữa Development và Operations. Các chỉ số quan trọng: MTTR (thời gian khôi phục trung bình) và tần suất triển khai.
- **AWS CI/CD Pipeline:**
    - **Source Control:** Quản lý mã nguồn với AWS CodeCommit (và các chiến lược GitFlow).
    - **Build & Test:** Cấu hình AWS CodeBuild để đóng gói ứng dụng.
    - **Deployment:** Các chiến lược triển khai an toàn (Blue/Green, Canary) với AWS CodeDeploy.
    - **Orchestration:** Tự động hóa toàn bộ quy trình bằng AWS CodePipeline.
- **IaC (Infrastructure as Code):** So sánh giữa CloudFormation (Templates) và AWS CDK (Code). Demo triển khai hạ tầng bằng CDK.

#### 2. Buổi chiều: Containers & Observability (13:00 – 17:00)
- **Container Services:**
    - Quản lý Docker images với **Amazon ECR**.
    - Điều phối container với **Amazon ECS** và **EKS**.
    - So sánh triển khai Microservices trên các nền tảng khác nhau.
- **Monitoring & Observability:**
    - Thiết lập Dashboard và Alarm với **Amazon CloudWatch**.
    - Truy vết phân tán (Distributed tracing) với **AWS X-Ray** để tìm điểm nghẽn hiệu năng.
- **Best Practices:** Các chiến lược quản lý sự cố và lộ trình chứng chỉ AWS DevOps.

### Điểm nhấn & Bài học (Key Takeaways)

#### IaC là "Game Changer"
- Trước đây nhóm em thường tạo tài nguyên bằng cách click trên Console (ClickOps), rất dễ sai sót và khó đồng bộ. Qua phần demo **AWS CDK**, em nhận ra sức mạnh của việc định nghĩa hạ tầng bằng ngôn ngữ lập trình (TypeScript/Python). Điều này giúp việc tái tạo môi trường (Dev/Test/Prod) trở nên dễ dàng và chính xác tuyệt đối.

#### CI/CD không chỉ là Deploy code
- Em học được rằng một pipeline chuẩn không chỉ là đẩy code lên server, mà còn phải bao gồm các bước **Automated Testing** và các chiến lược **Deployment an toàn** (như Blue/Green) để giảm thiểu rủi ro downtime cho người dùng cuối.

#### Observability quan trọng hơn Monitoring
- Monitoring chỉ cho biết "Hệ thống đang lỗi", còn Observability (với X-Ray) cho biết "Tại sao lỗi". Với kiến trúc Microservices của dự án hiện tại, việc tích hợp X-Ray là bắt buộc để debug hiệu quả.

### Hình ảnh sự kiện

![Tham gia Event](/images/4-Events/E3-1.jpeg)

![Tham gia Event](/images/4-Events/E3-2.jpeg)

![Tham gia Event](/images/4-Events/E3-3.jpeg)

![Tham gia Event](/images/4-Events/E3-4.jpeg)

### Cảm nhận cá nhân

Buổi workshop **DevOps on AWS** là mảnh ghép kỹ thuật quan trọng cuối cùng mà em đang thiếu cho dự án Group Project.

Nó giúp em hệ thống hóa lại toàn bộ quy trình phát triển phần mềm. Ngay sau buổi học, em đã có ý tưởng để refactor lại pipeline Gitlab CI hiện tại của nhóm, tích hợp thêm phần scan bảo mật ECR và tracing với X-Ray để chuẩn bị tốt nhất cho buổi Final Showcase sắp tới.

> **Lời kết:** Một ngày ngập trong kiến thức nhưng vô cùng giá trị. Giờ đây em đã tự tin hơn để nói rằng mình hiểu về quy trình DevOps chuẩn mực!