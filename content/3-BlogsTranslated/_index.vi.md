---
title: "Các bài blogs đã dịch"
date: 2025-10-07
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Tại đây là phần liệt kê và tóm tắt nội dung các bài blog kỹ thuật chuyên sâu về AWS mà tôi đã thực hiện dịch thuật và nghiên cứu.

### [Blog 1 - Bắt đầu với Data Lake trong Y tế: Sử dụng Microservices](3.1-Blog1/)
Blog này hướng dẫn cách xây dựng Data Lake trong lĩnh vực y tế bằng cách áp dụng kiến trúc Microservices. Bạn sẽ tìm hiểu cách xử lý các bản tin HL7v2 thông qua kiến trúc hướng sự kiện (Event-driven) với mô hình Pub/Sub Hub. Bài viết đi sâu vào việc sử dụng Amazon SNS, Lambda và DynamoDB để tạo ra hệ thống linh hoạt, dễ mở rộng và tách biệt các thành phần xử lý dữ liệu nhạy cảm.

### [Blog 2 - Đặc điểm của các workload HPC trong dịch vụ tài chính trên cloud](3.2-Blog2/)
Bài viết phân tích các thuộc tính kỹ thuật của các workload tính toán hiệu năng cao (HPC) trong ngành Dịch vụ Tài chính (FSI). Nội dung cung cấp một "cây quyết định" (decision tree) giúp các tổ chức lựa chọn nền tảng phù hợp trên AWS—từ việc di chuyển các scheduler cũ (như IBM Symphony) đến xây dựng giải pháp cloud-native (AWS Batch, AWS Lambda)—dựa trên thời lượng tác vụ và yêu cầu về thông lượng.

### [Blog 3 - AWS IoT Greengrass Nucleus Lite: Cách mạng hóa điện toán biên](3.3-Blog3/)
Giới thiệu Nucleus Lite, một edge runtime viết bằng ngôn ngữ C dành cho các thiết bị biên bị giới hạn tài nguyên (dưới 512MB RAM). Blog so sánh chi tiết giữa phiên bản Lite và phiên bản Java tiêu chuẩn (Nucleus), làm rõ các ưu điểm về dung lượng bộ nhớ thấp, cấp phát bộ nhớ tĩnh và khả năng tích hợp sâu với systemd trên các hệ thống Linux nhúng (Embedded Linux).

### [Blog 4 - Các chiến lược chủ động cho Cyber Resilience và Business Continuity](3.4-Blog4/)
Cung cấp hướng dẫn cho các tổ chức trong việc vận hành hệ thống bền vững trước các sự cố an ninh mạng (như ransomware) hoặc thảm họa thiên nhiên. Bài viết đề xuất các chiến lược cốt lõi như: triển khai môi trường đa tài khoản (multi-account), sử dụng Infrastructure as Code (IaC) để phục hồi nhanh, và duy trì các bản sao lưu bất biến (immutable backups) trong các tài khoản khôi phục biệt lập.

### [Blog 5 - Kiến trúc sư HPC tiết kiệm: Đảm bảo FinOps hiệu quả](3.5-Blog5/)
Khám phá các phương pháp hay nhất (best practices) để quản lý chi phí cho các workload HPC quy mô lớn trên AWS. Dựa trên nguyên lý "The Frugal Architect", bài viết thảo luận về hai chiến lược chính: giảm chi phí đơn vị (sử dụng EC2 Spot, Savings Plans, chip Graviton) và giảm mức tiêu thụ đơn vị (tối ưu hóa hiệu quả tính toán) để cân bằng giữa sự linh hoạt và ngân sách.