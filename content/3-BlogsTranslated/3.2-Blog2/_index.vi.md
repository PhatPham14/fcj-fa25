---
title: "AWS IoT Greengrass Nucleus Lite - Cách mạng hóa điện toán biên trên các thiết bị bị giới hạn tài nguyên"
date: 2025-04-15
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
tags:
  - AWS IoT
  - AWS IoT Greengrass V2
  - Edge Computing
  - IoT Edge
---

**Bởi Camilla Panni và Greg Breen**

[AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html) là phần mềm mã nguồn mở chạy ở biên (edge runtime) và dịch vụ cloud giúp bạn xây dựng, triển khai và quản lý các ứng dụng đa tiến trình ở quy mô lớn trên toàn bộ hạm đội thiết bị IoT.

Phiên bản AWS IoT Greengrass V2 được ra mắt vào tháng 12 năm 2020 với một Java edge runtime gọi là [nucleus](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-nucleus-component.html). Với [bản phát hành 2.14.0](https://docs.aws.amazon.com/greengrass/v2/developerguide/greengrass-release-2024-12-16.html) vào tháng 12 năm 2024, AWS giới thiệu thêm một tùy chọn edge runtime là **Nucleus Lite** - được viết bằng ngôn ngữ C.

**AWS IoT Greengrass Nucleus Lite** là một edge runtime [mã nguồn mở](https://github.com/aws-greengrass/aws-greengrass-lite), gọn nhẹ, hướng đến các thiết bị có giới hạn tài nguyên. Nó mở rộng khả năng của AWS IoT Greengrass đến các thiết bị giá rẻ, single-board computer phục vụ các ứng dụng như smart home hub, smart energy meter, smart vehicle, edge AI, và robotics.

Bài viết này giải thích ưu điểm của hai tùy chọn edge runtime và cung cấp hướng dẫn giúp bạn chọn lựa phương án phù hợp với trường hợp sử dụng.

---

### Sự khác biệt chính giữa Nucleus và Nucleus Lite

AWS IoT Greengrass Nucleus Lite hoàn toàn tương thích với AWS IoT Greengrass [V2 Cloud Service API](https://docs.aws.amazon.com/greengrass/v2/APIReference/API_Operations.html) và [IPC](https://docs.aws.amazon.com/greengrass/v2/developerguide/interprocess-communication.html) interface. Điều này có nghĩa là bạn có thể xây dựng và triển khai các component hướng đến một hoặc cả hai runtime. Tuy nhiên, Nucleus Lite có một số điểm khác biệt quan trọng:

#### 1. Memory footprint (Dung lượng bộ nhớ)

* **Nucleus (Java):** Yêu cầu tối thiểu 256 MB đĩa và 96 MB RAM. AWS khuyến nghị tối thiểu **512 MB RAM** để đáp ứng hệ điều hành, JVM và ứng dụng.
* **Nucleus Lite (C):** Yêu cầu ít hơn **5 MB RAM và 5 MB lưu trữ**, không phụ thuộc vào JVM và chỉ yêu cầu thư viện chuẩn C.

![pic 1](/images/3-Blog/B2-1.png)
> *Hình 1: Dung lượng bộ nhớ của Nucleus so với Nucleus Lite.*

Dung lượng nhỏ hơn này mở ra khả năng mới cho việc phát triển ứng dụng IoT trên các thiết bị bị giới hạn tài nguyên.

#### 2. Static memory allocation (Cấp phát bộ nhớ tĩnh)

Nucleus Lite cấp phát một lượng bộ nhớ cố định khi khởi động và giữ nguyên không đổi.
* **Lợi ích:** Yêu cầu tài nguyên có thể dự đoán được, giảm thiểu rủi ro rò rỉ bộ nhớ.
* **Hiệu năng:** Loại bỏ độ trễ không xác định (non-deterministic latency) thường gặp ở các ngôn ngữ có cơ chế thu gom rác (garbage-collected) như Java.

#### 3. Directory structure (Cấu trúc thư mục)

Nucleus Lite tách biệt rõ ràng các thành phần trên đĩa, hỗ trợ tối ưu cho **Embedded Linux**:

* **Runtime:** Có thể lưu trên phân vùng **Read-Only** (hỗ trợ cơ chế cập nhật A/B OS).
* **Components & Config:** Nằm ở phân vùng **Read-Write** hoặc overlay để quản lý qua deployment.
* **Logs:** Lưu trong phân vùng tạm thời hoặc ổ đĩa khác để tránh hao mòn bộ nhớ flash.

Cách tách biệt này giúp bạn tạo [golden image cho sản xuất thiết bị hàng loạt](https://docs.aws.amazon.com/prescriptive-guidance/latest/iot-greengrass-golden-images/introduction.html).

#### 4. Tích hợp với Systemd

[Systemd](https://systemd.io/) là yêu cầu bắt buộc đối với Nucleus Lite.
* Nucleus Lite được cài đặt như một bộ các dịch vụ systemd.
* Mỗi component được triển khai cũng chạy như một dịch vụ systemd riêng biệt.
* Việc ghi log được xử lý tập trung bởi systemd, cho phép dùng các công cụ Linux quen thuộc để debug.

---

### Lựa chọn giữa Nucleus và Nucleus Lite

Việc lựa chọn phụ thuộc vào trường hợp sử dụng, phần cứng và hệ điều hành. Bảng dưới đây tóm tắt các gợi ý:

| Khi nên dùng Nucleus (Java) | Khi nên dùng Nucleus Lite (C) |
| :--- | :--- |
| Bạn muốn dùng Windows hoặc bản Linux không có systemd | Thiết bị của bạn bị giới hạn bộ nhớ (**≤ 512 MB RAM**) |
| Ứng dụng của bạn chạy trong Docker containers | CPU thiết bị có tốc độ xung nhịp **< 1 GHz** |
| Thành phần ứng dụng là Lambda functions | Bạn tạo bản Embedded Linux cần kiểm soát chính xác phân vùng (OS updates, A/B partitions) |
| Bạn phát triển bằng ngôn ngữ script hoặc interpreted | Bạn lập trình bằng ngôn ngữ biên dịch sang mã máy |
| Bạn cần tính năng [chưa được hỗ trợ bởi Nucleus Lite](https://docs.aws.amazon.com/greengrass/v2/developerguide/operating-system-feature-support-matrix.html) | Bạn có yêu cầu tuân thủ không cho phép dùng Java |
| Bạn tạo [AWS IoT SiteWise gateway](https://docs.aws.amazon.com/iot-sitewise/latest/userguide/gw-self-host-gg2.html) | Bạn ưu tiên cấp phát bộ nhớ tĩnh (static memory allocation) |

> *Bảng 1: Hướng dẫn chọn giữa Nucleus và Nucleus Lite.*

---

### Use case và kịch bản triển khai

#### 1. Các trường hợp sử dụng (Use cases)
Với yêu cầu tài nguyên thấp, Nucleus Lite phù hợp cho các thiết bị chi phí thấp, bộ nhớ và CPU hạn chế trong các lĩnh vực như nhà thông minh, công nghiệp, ô tô, và đo lường thông minh.

#### 2. Embedded systems (Hệ thống nhúng)
Nucleus Lite hỗ trợ Embedded Linux ngay từ đầu thông qua dự án [meta-aws](https://github.com/aws4embeddedlinux/meta-aws). Dự án này cung cấp các "recipes" để tích hợp vào Yocto/OpenEmbedded, và kho [meta-aws-demos](https://github.com/aws4embeddedlinux/meta-aws-demos) chứa các ví dụ như cập nhật A/B với RAUC.

#### 3. Multi-tenancy với containerized Nucleus Lite
Với dung lượng nhỏ gọn, Nucleus Lite mang lại khả năng container hóa hiệu quả cho mô hình đa người dùng (multi-tenant).

![pic 1](/images/3-Blog/B2-2.png)

> *Hình 2: Container hóa đa người dùng (Multi-tenant containerization).*

* **Cô lập an toàn:** Mỗi instance container duy trì ranh giới chặt chẽ.
* **Tối ưu tài nguyên:** Dung lượng nhỏ cho phép nhiều container hoạt động trên thiết bị giới hạn.
* **Hoạt động độc lập:** Các ứng dụng được quản lý và cập nhật riêng biệt.

---

### Best practices

**1. Plugin compatibility:**
Các Nucleus plugin (viết bằng Java cho runtime gốc) **không thể** sử dụng với runtime Nucleus Lite.

**2. Lựa chọn ngôn ngữ Component:**
* Chọn Python/Java sẽ làm giảm lợi thế tiết kiệm bộ nhớ của Nucleus Lite (do cần interpreter hoặc JVM).
* **Khuyến nghị:** Viết lại các thành phần quan trọng bằng **C, C++, hoặc Rust** để đạt hiệu suất tối đa.

**3. Chuyển đổi và Phát triển:**
* Khi chuyển đổi: Có thể chạy component hiện có "as-is" để đảm bảo chức năng trước khi tối ưu.
* Khi phân bổ ngân sách bộ nhớ (memory budget): Cần tính toán toàn bộ các phụ thuộc runtime và footprint hệ thống, không chỉ riêng Nucleus Lite.

---

### Tương lai và kết luận

AWS IoT Greengrass Nucleus Lite giúp tái tưởng tượng cách triển khai điện toán biên bằng cách giảm đáng kể yêu cầu tài nguyên. Điều này cho phép:
* Triển khai IoT trên phần cứng rẻ hơn, đa dạng hơn.
* Giảm chi phí vận hành.
* Kích hoạt các use case mới trước đây không khả thi.

Sẵn sàng bắt đầu?
* **Khám phá:** [Tài liệu AWS IoT Greengrass](https://docs.aws.amazon.com/greengrass/v2/developerguide/what-is-iot-greengrass.html).
* **Thực hành:** [Hướng dẫn cài đặt](https://github.com/aws-greengrass/aws-greengrass-lite/blob/main/docs/SETUP.md#setting-up-greengrass-nucleus-lite).
* **Cộng đồng:** Tham gia diễn đàn [AWS IoT Community](https://repost.aws/topics/TAEQXJMLWWTp2elx_Bkb1Kvw/internet-of-things-iot).
* **Đóng góp:** Gửi mã nguồn lên [Github repo](https://github.com/aws-greengrass/aws-greengrass-lite).

---

#### Về tác giả

> **Camilla Panni**
>
> Kiến trúc sư Giải pháp (Solutions Architect) tại AWS. Cô hỗ trợ khách hàng khu vực công tại Ý tăng tốc chuyển đổi đám mây. Camilla có nền tảng kỹ thuật về tự động hóa và IoT.

> **Greg Breen**
>
> Kiến trúc sư Giải pháp Chuyên gia IoT Cấp cao tại AWS, làm việc tại Úc. Với kinh nghiệm chuyên sâu về hệ thống nhúng, Greg hỗ trợ các nhóm phát triển sản phẩm tại khu vực Châu Á - Thái Bình Dương đưa thiết bị ra thị trường.