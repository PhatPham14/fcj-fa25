---
title: "Đặc điểm của các workload HPC trong dịch vụ tài chính trên cloud"
date: 2025-04-15
weight: 10
chapter: false
pre: " <b> 2.1. </b> "
tags:
  - FSI
  - HPC
  - Best Practices
---

**Bởi Mark Norton và Flamur Gogolli**

Bài đăng này giới thiệu các yêu cầu của High Performance Computing (HPC) trong ngành Dịch vụ Tài chính (FSI). Nó định nghĩa các thuộc tính kỹ thuật của các workload nặng về tính toán (compute-heavy) và cung cấp quy trình cây quyết định (decision tree) để giúp khách hàng chọn nền tảng HPC phù hợp trên AWS.

---

### HPC trong Dịch vụ Tài chính

Trong lĩnh vực dịch vụ tài chính, HPC (hay Grid computing) từ lâu đã được sử dụng để chạy mô phỏng và giải quyết các bài toán phức tạp.

* **Thị trường vốn (Capital Markets):** Định giá công cụ tài chính (stocks, ETFs, derivatives, bonds) bằng mô hình Monte Carlo. Các workload trải dài từ tính toán thời gian thực/intraday nhạy với độ trễ đến các batch lớn chạy qua đêm (overnight risk monitoring).
* **Quản lý đầu tư:** Phân tích rủi ro, tính toán exposure, tối ưu hóa và back-testing chiến lược hedging.
* **Bảo hiểm:** Mô hình định phí (actuarial modeling) và mô phỏng thiên tai để xác định mức phí và chiến lược giảm thiểu rủi ro.

---

### Cloud Adoption Patterns trong FSI

Các tổ chức tài chính thường di chuyển nền tảng HPC lên cloud theo từng giai đoạn để đáp ứng nhu cầu tài nguyên biến động (ví dụ: báo cáo cuối quý).



Dưới đây là các mức độ adopt cloud phổ biến:

1.  **All On-premises:** Scheduler, compute và dữ liệu hoàn toàn tại chỗ.
2.  **Hybrid Burst:** Mở rộng compute capacity lên cloud khi nhu cầu on-premises quá tải.
3.  **Lift and Shift:** Di chuyển nguyên trạng scheduler và compute node lên cloud.
4.  **AWS Optimized:** Tăng cường tính đàn hồi (elasticity), sử dụng managed services và tối ưu mô hình mua (Spot, Savings Plans).
5.  **AWS Native:** Tái thiết kế toàn bộ sử dụng kiến trúc serverless, scheduler hiện đại và phần cứng tối ưu (AI accelerators, chip thế hệ mới).

---

### Đặc điểm Workload để quyết định kiến trúc

Để chọn nền tảng phù hợp, cần xem xét các đặc điểm sau của workload:

* **Task Duration:** Từ vài giây đến hàng ngày.
* **High Throughput:** Hàng chục nghìn task/giây.
* **Parallelization:** Khả năng chạy song song (loosely coupled).
* **Resource Intensity:** Tỷ lệ CPU/Memory/IO.
* **Software Requirements:** OS, thư viện, dependencies.
* **Cost Optimization:** Cân bằng giữa hiệu suất và chi phí.

Sử dụng cây quyết định dưới đây để chọn giải pháp phù hợp:



> *Hình 1. Decision tree để chọn giải pháp HPC cho cloud dựa trên các đặc điểm workload.*

Quyết định quan trọng nhất bắt đầu bằng việc: **Giữ lại Scheduler hiện có (On-prem)** hay **Xây dựng giải pháp Cloud-native mới**.

---

### 1. Di chuyển Scheduler hiện có lên Cloud

Nếu bạn chọn giữ scheduler Grid hiện có do lo ngại về công sức di chuyển hoặc yêu cầu dự án:

* **Scheduler thương mại:** IBM Spectrum Symphony, TIBCO DataSynapse GridServer®.
* **Scheduler Open-source:** Slurm Workload Manager, HTCondor.

Cách tiếp cận thường là **Hybrid Burst** hoặc **Lift-and-Shift**. Mặc dù mang lại giao diện quen thuộc, phương pháp này vẫn giữ lại các hạn chế cũ về license và quản lý hạ tầng phức tạp.

### 2. Xây dựng và sử dụng Scheduler Cloud-Native

Phương pháp này giúp giảm gánh nặng vận hành và tận dụng tối đa lợi ích cloud. Quyết định sẽ dựa trên **Task Duration**:

#### A. Hỗn hợp task ngắn và dài (Vài giây - Vài phút)
* **Slurm trên AWS:** Sử dụng **AWS ParallelCluster** (quản lý cluster open-source) hoặc **AWS Parallel Computing Service** (managed service hoàn toàn).

#### B. Task dài (> 1 phút)
* **AWS Batch:** Dịch vụ batch computing quản lý hoàn toàn. Bạn không tốn phí scheduler, chỉ trả tiền cho tài nguyên compute.

#### C. High Throughput (Task giây - phút)
* **HTC-Grid:** Một dự án cộng đồng (ban đầu từ AWS, nay thuộc FINOS) dành cho nhu cầu xử lý hàng chục nghìn task mỗi giây.

#### D. Task cực ngắn (< 15 phút)
* **AWS Lambda:** Tận dụng kiến trúc serverless, không cần quản lý server "always-on", phù hợp cho throughput cao nhưng bị giới hạn cứng về thời gian chạy.



---

### Kết luận & Những điểm chính

Không có giải pháp "one-size-fits-all". Việc lựa chọn phụ thuộc vào chiến lược của bạn:

1.  **Duy trì Scheduler hiện có:**
    * *Thương mại:* IBM Symphony, Tibco (Ổn định nhưng thiếu linh hoạt).
    * *Open-source:* Slurm, HTCondor (Dùng AWS ParallelCluster để quản lý tốt hơn).

2.  **Chuyển sang Cloud-Native:**
    * *Workload > 5 phút:* **AWS Batch**.
    * *Workload < 15 phút:* **AWS Lambda**.
    * *High throughput (giây-phút):* **HTC-Grid** hoặc giải pháp Container-based.

Hãy xem đây là điểm khởi đầu của hành trình. Bạn có thể bắt đầu từ "Lift & Shift" và dần dần tối ưu hóa để trở thành "AWS Native".

---

#### Về tác giả

> **Mark Norton**
>
> Chuyên gia HPC Cấp cao tại AWS với hơn 30 năm kinh nghiệm. Ông chuyên thiết kế các giải pháp cloud mở rộng cho ngành tài chính, ô tô và nghiên cứu.

> **Flamur Gogolli**
>
> Kiến trúc sư Giải pháp Chuyên gia Cấp cao tại AWS. Cựu nhân sự tại JP Morgan, có kinh nghiệm sâu rộng về hiện đại hóa hạ tầng, Cloud-native, Container và DevOps.