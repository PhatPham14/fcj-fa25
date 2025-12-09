---
title: "Đặc điểm của các workload HPC trong dịch vụ tài chính trên cloud"
date: 2025-04-15
weight: 10
chapter: false
pre: " <b> 3.1. </b> "
tags:
  - FSI
  - HPC
  - Best Practices
---

**Bởi Mark Norton và Flamur Gogolli**

Bài đăng này giới thiệu các yêu cầu của High Performance Computing (HPC) trong ngành Dịch vụ Tài chính (Financial Services Industry - FSI). Nó định nghĩa các thuộc tính kỹ thuật của các workload nặng về compute và thảo luận các đặc điểm thiết yếu của chúng. Thêm vào đó, nó cung cấp một quy trình decision tree để giúp khách hàng chọn nền tảng HPC phù hợp trên cloud dù là vendor thương mại, open-source, hoặc giải pháp cloud-native dựa trên yêu cầu của khách hàng và workload.

Mặc dù không thể bao phủ tất cả các lựa chọn khả thi, bài viết này cung cấp hướng dẫn về cách đạt được mục tiêu price-performance và giải quyết các thách thức HPC bằng cách sử dụng các dịch vụ và giải pháp của AWS, dựa trên kinh nghiệm với các khách hàng trong ngành Dịch vụ Tài chính.

Trong lĩnh vực dịch vụ tài chính, HPC (hoặc còn được gọi là Grid computing) đã từ lâu được sử dụng để chạy mô phỏng và giải quyết các thách thức phức tạp.
* **Thị trường vốn:** Hệ thống HPC được sử dụng để định giá các công cụ tài chính (ví dụ: stocks, ETFs, derivatives, bonds) bằng các mô hình toán như [Monte Carlo](https://aws.amazon.com/what-is/monte-carlo-simulation/). Các mô hình sử dụng trải dài từ các phép tính thời gian thực/intraday nhạy với độ trễ đến các workload batch lớn thường diễn ra qua đêm.
* **Quản lý đầu tư:** Sử dụng HPC cho định giá và phân tích rủi ro, tính toán exposure, tối ưu hóa và back-testing chiến lược hedging.
* **Bảo hiểm:** Mô hình định phí (actuarial modeling) và mô phỏng thiên tai để xác định mức phí và chiến lược giảm thiểu rủi ro.

---

### Cloud adoption patterns in FSI

Các tổ chức tài chính phải đối mặt với nhu cầu ngày càng tăng đối với tài nguyên HPC do yêu cầu quy định, biến động thị trường và nhu cầu báo cáo - đòi hỏi dung lượng lớn trong các giai đoạn như xử lý qua đêm hoặc báo cáo cuối quý.

Nhiều tổ chức chuyển từ hạ tầng tại chỗ (on-premises) sang cloud để mở rộng tài nguyên linh hoạt và tối ưu hóa chi phí. Khách hàng FSI thường di chuyển nền tảng HPC của họ lên cloud theo từng giai đoạn:

* **All On-premises:** Scheduler, compute, và nguồn dữ liệu được host tại chỗ.
* **Hybrid Burst:** Scheduler, compute và dữ liệu nằm on-premises nhưng được bổ sung bằng compute capacity trên cloud khi có nhu cầu cao hoặc đột biến.
* **Lift and Shift:** Scheduler hiện có được chuyển nguyên trạng (as-is) lên cloud và chạy các compute node trên cloud với cấu hình tương tự on-premises.
* **AWS Optimized:** Trọng tâm là tính elasticity của compute và sử dụng các dịch vụ quản lý (managed services) kết hợp với các mô hình mua (Amazon EC2 Spot, Savings Plans).
* **AWS Native:** Tái tưởng tượng hoàn toàn các nền tảng HPC truyền thống, sử dụng kiến trúc cloud-native, serverless và phần cứng tối ưu (AI accelerators).

---

### Đặc điểm workload để quyết định kiến trúc

Các workload HPC trong FSI có yêu cầu đa dạng, tuy nhiên có một số đặc điểm chung quan trọng:

* **Varying Task Duration:** Từ vài giây đến hàng giờ hoặc thậm chí ngày.
* **High Throughput Requirements:** Thường cần xử lý hàng chục nghìn task mỗi giây.
* **High Parallelization Requirements:** Hầu hết các phép tính thường loosely coupled, cho phép chạy song song.
* **Resource Intensity:** Tỷ lệ CPU : Memory và yêu cầu I/O.
* **Software Requirements:** Hệ điều hành, nền tảng và thư viện.
* **Data & Application Dependencies:** Xử lý cục bộ vs phân tán.
* **Elasticity & Flexibility:** Khả năng scale lên xuống theo nhu cầu.
* **Cost Optimization:** Cân bằng giữa hiệu suất và chi phí.

Chúng ta sẽ sử dụng decision tree trong Hình 1 để hướng dẫn lựa chọn nền tảng phù hợp.

[Image placeholder: Decision tree để chọn giải pháp HPC cho cloud dựa trên các đặc điểm workload]
> *Hình 1. Decision tree để chọn giải pháp HPC cho cloud dựa trên các đặc điểm workload.*

Việc điều hướng bắt đầu với quyết định quan trọng: **Giữ scheduler on-premises hiện có** hay **Xây dựng giải pháp cloud-native mới**.

#### 1. Migrating your existing scheduler to the cloud

Nếu bạn chọn giữ scheduler Grid hiện có do lo ngại về công sức di chuyển hoặc tiến độ dự án:

* **Scheduler thương mại:** [IBM Spectrum Symphony](https://www.ibm.com/products/analytics-workload-management) hoặc [TIBCO DataSynapse GridServer®](https://docs.tibco.com/products/tibco-datasynapse-gridserver-manager-7-1-0).
* **Scheduler Open-source:** [Slurm Workload Manager](https://slurm.schedmd.com/documentation.html) hoặc [HTCondor](https://htcondor.org/).

Các phương thức di chuyển thường gặp:
* **Hybrid Burst:** Dùng AWS để bổ sung cho grid on-premises khi cao điểm.
* **Lift-and-Shift:** Di chuyển toàn bộ hệ thống lên AWS "as-is".

#### 2. Xây dựng và sử dụng scheduler / nền tảng HPC cloud-native

Đây là hướng tiếp cận để giải quyết các hạn chế cũ và tận dụng tối đa cloud. Quyết định sẽ dựa nhiều vào **Task Duration**:

* **Hỗn hợp task ngắn/dài (Giây - Phút):**
    * Nếu quen dùng Slurm: Sử dụng [AWS ParallelCluster](https://aws.amazon.com/hpc/parallelcluster/) hoặc [AWS Parallel Computing Service](https://aws.amazon.com/pcs/) (managed service).
* **Task dài (> 1 phút):**
    * Sử dụng [AWS Batch](https://aws.amazon.com/batch/), dịch vụ batch computing quản lý hoàn toàn (miễn phí scheduler, chỉ trả tiền tài nguyên compute).
* **High Throughput (Giây - Phút):**
    * Sử dụng [HTC-Grid](https://github.com/finos/htc-grid), một dự án cộng đồng (FINOS) có khả năng xử lý hàng chục nghìn task mỗi giây.
* **Task cực ngắn (< 15 phút):**
    * Tận dụng kiến trúc serverless với [AWS Lambda](https://aws.amazon.com/lambda/). Không cần quản lý server "always-on", throughput cao nhưng bị giới hạn cứng về thời gian chạy.

---

### Kết luận

Không có một giải pháp "one-size-fits-all". Số lượng task và thời gian chạy sẽ quyết định giải pháp phù hợp nhất.

Hãy xem việc lựa chọn nền tảng là điểm khởi đầu của hành trình. Chúng tôi thấy khách hàng thường tiếp tục hành trình từ "Lift & Shift" đến "AWS Optimized" và "AWS Native" để tối ưu hóa liên tục.

### Những điểm chính cần ghi nhớ

1.  **Nếu duy trì scheduler hiện có:**
    * Giải pháp thương mại (IBM, Tibco) ổn định nhưng thiếu linh hoạt cloud.
    * Open-source (Slurm, HTCondor) có thể dùng AWS ParallelCluster/PCS để quản