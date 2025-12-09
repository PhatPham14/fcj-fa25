---
title: "Kiến trúc sư HPC tiết kiệm – đảm bảo FinOps hiệu quả cho workloads HPC quy mô lớn"
date: 2025-04-08
weight: 2
chapter: false
pre: " <b> 3.4. </b> "
tags:
  - HPC
  - FinOps
  - Best Practices
---

**Bởi Alex Kimber**

![pic 1](/images/3-Blog/B3-1.png)

Việc áp dụng tính toán linh hoạt, theo yêu cầu và có thể mở rộng trên cloud mang lại nhiều lợi ích. Nó giải phóng các tổ chức khỏi các quy trình mua sắm kéo dài và lặp đi lặp lại liên quan đến cơ sở hạ tầng tại chỗ, vốn thường yêu cầu ước tính giáo dục để xác định kích thước, và kết quả là cơ sở hạ tầng chỉ tốt như ngày nó được cài đặt. Trong khi trọng tâm của bài viết này là giảm chi phí, cũng quan trọng là nhận ra các cơ hội mà việc thử nghiệm ở quy mô lớn có thể mở khóa. Cloud cho phép khách hàng đạt được các mức độ quy mô mà sẽ không thể tài chính hóa với cơ sở hạ tầng tại chỗ vì nó có thể được cấp phát cho thời gian của bất kỳ workload cá nhân nào và sau đó được giải phóng. Tuy nhiên, với việc cấp phát linh hoạt trên cloud đi kèm với sự biến động chi phí có thể khiến các tổ chức có ngân sách cố định hoặc biên lợi nhuận chặt chẽ cảm thấy lo ngại.

Trong bài viết này, chúng tôi sẽ khám phá các best practices mà chúng tôi đã thấy từ công việc của mình với khách hàng từ các ngành công nghiệp khác nhau đang chạy workloads HPC ở quy mô lớn. Thêm vào đó, chúng tôi sẽ tham khảo hướng dẫn từ Werner Vogels, một nhà lãnh đạo ngành đã phát triển ['The Frugal Architect'](https://thefrugalarchitect.com/) để giúp các tổ chức suy nghĩ về những thách thức này và tìm ra sự cân bằng đúng đắn giữa các yêu cầu tương hỗ về tính linh hoạt, hiệu quả và hiệu suất của hệ thống.

### HPC và cloud

Các hệ thống tính toán hiệu suất cao (HPC) ngày càng trở nên phổ biến trên AWS và là một trong những workloads đầu tiên tận dụng khả năng tính toán linh hoạt ở quy mô lớn, cho dù là bổ sung năng lực tại chỗ với các mô hình 'burst' hay là nơi chính để tính toán quy mô lớn. Mặc dù các bài học từ The Frugal Architect có tính ứng dụng rộng rãi, nhưng có một số bài học đặc biệt áp dụng cho workloads HPC.



HPC bao gồm cả các hệ thống liên kết chặt chẽ chạy các workloads như động lực học chất lỏng tính toán (CFD), hoặc các hệ thống liên kết lỏng lẻo khổng lồ có thể chạy các mô hình tài chính. Cả hai đều có khả năng tạo ra chi phí đáng kể cho người tiêu dùng của chúng, vì vậy việc xem xét cẩn thận thiết kế, đo lường và khả năng quan sát của các hệ thống này càng quan trọng hơn. Bài viết này sẽ tập trung vào các cơ hội cho các workloads liên kết lỏng lẻo nhưng nhiều trong số này sẽ áp dụng cho bất kỳ workload HPC nào.

### Chi phí và các công cụ tiết kiệm

'Định lý' đầu tiên của The Frugal Architect là **“Làm cho chi phí trở thành một yêu cầu phi chức năng”**, nhấn mạnh tầm quan trọng của việc xem xét chi phí cùng với các yêu cầu khác như bảo mật, khả năng truy cập, tuân thủ và khả năng bảo trì như các thước đo thành công của một hệ thống.

Trong mô hình cấp phát 'pay as you go', chi phí là sản phẩm của chi phí đơn vị và số lượng đơn vị tiêu thụ. Việc tối ưu hóa có thể đến từ việc giảm chi phí của một đơn vị nhất định, bằng cách tiêu thụ ít đơn vị hơn – hoặc cả hai. Bạn có thể đạt được điều này theo nhiều cách khác nhau cho các hệ thống HPC chạy trên cloud, và AWS có các dịch vụ và tính năng để hỗ trợ mỗi phương pháp.

#### Giảm chi phí đơn vị

AWS cung cấp nhiều cơ hội để giảm chi phí đơn vị khi sử dụng các dịch vụ của mình. Mỗi chiến lược này đều có các đánh đổi, có thể hoặc không ảnh hưởng đến hiệu suất ứng dụng, nhưng một khi được đánh giá và triển khai, có thể mang lại lợi ích đáng kể.

Một trong những ví dụ có ảnh hưởng lớn về cơ hội giảm chi phí đơn vị tính toán là [Amazon EC2 Spot](https://aws.amazon.com/ec2/spot/), cho phép khách hàng tiết kiệm lên đến 90% so với cấp phát theo yêu cầu cho cùng một năng lực tính toán. Đánh đổi với EC2 Spot là các phiên bản này đến từ các nhóm sẵn sàng phục vụ người tiêu dùng năng lực theo yêu cầu và do đó chúng có thể bị AWS thu hồi bất kỳ lúc nào với cảnh báo 2 phút. Các workloads HPC có thể chấp nhận gián đoạn ngắt quãng (hoặc vì các tác vụ cá nhân là ngắn, hoặc vì chúng có thể checkpoint tiến trình của mình) có thể nhận được tiết kiệm đáng kể với EC2 Spot với gián đoạn tối thiểu.

Cũng có các đề nghị thương mại cho khách hàng có một mức độ nhu cầu ổn định. Trong kịch bản này, [Amazon EC2 Savings Plan](https://aws.amazon.com/savingsplans/compute-pricing/) cho phép khách hàng tiết kiệm lên đến 72% đổi lại việc cam kết năng lực đó trong 1 hoặc 3 năm. Thường thì khách hàng sẽ kết hợp EC2 Spot, Savings Plans và năng lực theo yêu cầu để đạt được sự kết hợp tối ưu.

Ngoài các giải pháp thương mại, còn có các cơ hội kỹ thuật để giảm chi phí đơn vị tính toán bằng cách đảm bảo bạn chỉ cấp phát những gì bạn cần. AWS hiện cung cấp hơn 750 loại phiên bản EC2 và do đó khách hàng có thể tìm thấy loại phiên bản phù hợp với workload của mình. Điều này đại diện cho một sự thay đổi so với cấp phát tại chỗ truyền thống, nơi các triển khai đồng nhất được sử dụng để hỗ trợ bộ tác vụ rộng nhất có thể. Trên cloud, mỗi workload có thể cấp phát sự kết hợp phù hợp của CPU, GPU, bộ nhớ, lưu trữ và hiệu suất mạng, tránh phải trả tiền cho các khả năng và tính năng không sử dụng.

Ngoài các phiên bản tính toán, AWS cung cấp một loạt các dịch vụ lưu trữ dữ liệu mang lại cơ hội giảm chi phí đơn vị lưu trữ dữ liệu. Ví dụ, tùy thuộc vào đặc điểm của một workload nhất định, có thể tối ưu khi sử [dụng Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) – có thể với [Mountpoint](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mountpoint.html) nếu bạn cần truy cập POSIX – thay vì một hệ thống tệp mạng truyền thống. Từ đó, bạn có thể khám phá các dịch vụ như [Amazon S3 Intelligent-Tiering](https://aws.amazon.com/s3/storage-classes/intelligent-tiering/) để giảm thêm chi phí đơn vị mỗi GB lưu trữ nếu có các tệp ít được truy cập.

Đối với mỗi ứng dụng, có thể có một số cơ hội để giảm chi phí đơn vị của tài nguyên trên AWS. Bằng cách phân tích các lợi ích tiềm năng và đánh đổi, bạn có thể ưu tiên các tùy chọn và khám phá những tùy chọn có lợi ích tiềm năng nhất cho bất kỳ workload cá nhân nào, tránh cách tiếp cận 'một kích cỡ phù hợp với tất cả'.

#### Giảm tiêu thụ đơn vị

Các đơn vị tiêu thụ sẽ thay đổi tùy thuộc vào dịch vụ AWS mà bạn đang sử dụng. Một số dịch vụ thậm chí có nhiều loại đơn vị, bao gồm các kiểu sử dụng khác nhau (ví dụ: Amazon S3 có đơn vị tiêu thụ cho các thao tác GET cũng như cho GB dữ liệu được lưu trữ).

Có một số cách hiệu quả để giảm tiêu thụ đơn vị core-hour của Amazon EC2, ví dụ, bạn có thể tăng hiệu quả bằng cách đảm bảo rằng – càng nhiều càng tốt – các core đang thực hiện các tác vụ tính toán và không bị nhàn rỗi hoặc làm việc trên các hoạt động không phải tính toán. Hoặc bạn có thể theo dõi hiệu quả bằng cách đảm bảo giá trị của công việc đang thực hiện vượt quá chi phí của tài nguyên compute được cấp phát; nếu không, hãy cân nhắc không chạy workload đó. Điều này phù hợp với định lý thứ hai của The Frugal Architect – **“Các hệ thống tồn tại lâu dài liên kết chi phí với doanh thu”**, đảm bảo rằng bất kỳ sự gia tăng chi phí nào đều được hiểu trong bối cảnh doanh thu.

Trọng tâm vào hiệu quả và hiệu suất đại diện cho một sự khác biệt đáng kể so với lập lịch tác vụ tại chỗ, nơi năng lực là tĩnh. Trong kịch bản đó, các workloads giá trị thấp hoặc không hiệu quả có thể được chấp nhận vì chúng không phát sinh chi phí bổ sung và có thể được chạy ở mức ưu tiên thấp. Trong khi điều này cũng đúng trên cloud khi năng lực được bao phủ bởi Savings Plan, bất kỳ năng lực bổ sung nào được cấp phát sẽ mang lại chi phí bổ sung cần được đánh giá so với giá trị doanh thu.

Một nhóm phương pháp để giảm tiêu thụ đơn vị compute là phân tích vòng đời tính phí của một instance AWS, từ lúc hệ điều hành (OS) bắt đầu khởi động cho đến khi kết thúc. Thời gian này có thể bao gồm các hoạt động overhead như: khởi động OS, tải và cài đặt các tệp nhị phân, khởi chạy agent HPC client, kết nối với scheduler, thời gian nhàn rỗi không có tác vụ, hoặc các tác vụ đang chờ dữ liệu phụ thuộc. Bằng cách giảm thiểu thời gian dành cho overhead và tối đa hóa thời gian dành cho tính toán hữu ích, bạn có thể cải thiện hiệu quả hệ thống, giảm số đơn vị compute cần cho workload nhất định.

Chi phí tổng thời gian khởi động OS có thể giảm bằng cách: tối ưu hóa các tiến trình khởi động riêng lẻ, giảm số lần khởi động instance bằng cách sử dụng On-Demand Instances chạy lâu dài, hoặc đa dạng hóa lựa chọn instance để giảm thiểu các sự kiện EC2 Spot Interruption yêu cầu khởi chạy instance thay thế. Các core CPU đang chờ dữ liệu có thể được giữ bận bằng một mức độ oversubscription của tác vụ, ví dụ chạy 10 threads trên hệ thống có 8 vCPUs.

Các instance AWS Graviton dựa trên Arm có thể mang lại lợi ích giá/hiệu suất đáng kể so với các instance x86 chạy workloads HPC. Các instance Graviton cung cấp hiệu suất giá tốt hơn đến 40% trong khi sử dụng ít năng lượng hơn đến 60% so với các instance EC2 tương đương. Vì các processor AWS Graviton thực hiện tập lệnh Arm64, bạn có thể cần thực hiện một số bước để port ứng dụng, nhưng AWS cung cấp [AWS Porting Advisor cho Graviton](https://github.com/aws/porting-advisor-for-graviton) để hỗ trợ việc này. Bạn có thể theo dõi tác động của việc áp dụng Graviton bằng [AWS Graviton Savings Dashboard](https://aws.amazon.com/ec2/graviton/graviton-savings-dashboard/). Lợi ích hiệu suất từ Graviton có thể giúp bạn hoàn thành workload nhanh hơn với cùng chi phí, hoặc giảm chi phí bằng cách cấp phát ít instance hơn cho cùng thời gian.

Một chỉ số tốt để đánh giá thành công trong việc giảm tiêu thụ đơn vị là CPU utilization. Nếu các instance Amazon EC2 của bạn có các giai đoạn sử dụng thấp đáng kể, thì có thể bạn chỉ cần sử dụng ít instance hơn, nhưng chạy ở mức sử dụng cao hơn.

Các ứng dụng HPC sử dụng dữ liệu lớn cũng có thể hưởng lợi từ cơ hội giảm tiêu thụ lưu trữ hiệu suất cao. Ví dụ, nhiều workloads HPC trên cloud sử dụng [Amazon FSx for Lustre](https://aws.amazon.com/fsx/lustre/) filesystem, cung cấp throughput hàng trăm GB/s và hàng triệu IOPS. Nhưng việc lưu trữ toàn bộ dataset trên Lustre có thể không hợp lý. Thường thì khách hàng [liên kết filesystem với Amazon S3](https://docs.aws.amazon.com/fsx/latest/LustreGuide/create-dra-linked-data-repo.html). Với cách này, FSx for Lustre hiển thị các đối tượng Amazon S3 dưới dạng file, có thể import vào Lustre theo nhu cầu. Điều này giảm đáng kể kích thước filesystem Lustre trong khi vẫn duy trì hiệu suất cao. Giảm thêm có thể đạt được bằng cách bật [Lustre data compression](https://docs.aws.amazon.com/fsx/latest/LustreGuide/data-compression.html), giảm dung lượng filesystem cần cho dataset nhất định.

Một phương pháp khác là sử dụng [Amazon File Cache](https://aws.amazon.com/filecache/), cung cấp truy cập hiệu suất cao tới Amazon S3 object storage, đồng thời cache các file lưu trong on-premises NFSv3 filesystem, giảm chi phí lưu trữ dữ liệu trùng lặp trên cloud. Tiết kiệm thêm có thể đạt được cho cả Amazon File Cache và FSx for Lustre bằng cách tắt khi không sử dụng và tái tạo khi nhu cầu trở lại.

### Observability

Định lý thứ tư của The Frugal Architect là **“Unobserved Systems lead to unknown costs”**. Trong phần trước, chúng ta đã giới thiệu các khái niệm cốt lõi về efficiency (đảm bảo tài nguyên cấp phát dành ít thời gian nhất cho công việc overhead) và effectiveness (đảm bảo giá trị công việc vượt quá chi phí tài nguyên compute được cấp phát).

Cả hai đều khó đánh giá nếu không có hệ thống observability, giúp HPC managers biết hiệu quả tổng thể thông qua các chỉ số như computation as a percentage of capacity provisioned, và cho khách hàng biết hiệu quả thông qua measures of business value as a percentage of cost to compute (hy vọng trên 100%).

Bằng cách cung cấp các chỉ số này kịp thời và chi tiết, stakeholders có thể nhận diện và định lượng các cơ hội cải tiến liên tục, đo lường kết quả của thay đổi, và phát hiện các kết quả bất ngờ nhanh chóng. AWS cung cấp nhiều công cụ hỗ trợ observability trên metrics, logs và traces, ví dụ [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) hoặc [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/).

Cũng quan trọng là có sự nhìn rõ ràng về chi phí (và nếu có thể, attribution của chi phí), và có công cụ hỗ trợ truy cập, phân tích và hiểu dữ liệu chi phí. Ví dụ, [AWS Data Exports](https://aws.amazon.com/aws-cost-management/aws-data-exports/) cho phép xuất dữ liệu theo chuẩn FinOps Open Cost and Usage Specification ([FOCUS](https://focus.finops.org/)) 1.0, có thể xử lý bằng giải pháp báo cáo hiện có hoặc trực quan hóa với [Amazon QuickSight](https://aws.amazon.com/quicksight). [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) cũng cho phép khám phá chi phí chi tiết, từ tổng quan đến phân tích sâu để nhận diện xu hướng, bất thường, hoặc các yếu tố chi phí chính.

Cuối cùng, [AWS Compute Optimizer](https://aws.amazon.com/compute-optimizer/) giúp xác định tài nguyên underutilized và đề xuất cách giải quyết. Ví dụ, có thể đề xuất chọn instance với ít memory hơn nếu provision hiện tại chưa sử dụng hết. Các đề xuất đi kèm với tiềm năng tiết kiệm để bạn ra quyết định tốt hơn.

### Kết luận

Khi lập kế hoạch migration hoặc mở rộng workload HPC lên cloud, chi phí cần được xem xét cùng các yêu cầu phi chức năng khác. Bài viết này khám phá sự thay đổi trong các driver chi phí khi đưa hệ thống vào cloud, và các cơ chế áp dụng cho clusters on-premises có thể không còn phù hợp.

HPC systems có thể hưởng lợi lớn từ tính linh hoạt và khả năng mở rộng của AWS Cloud; chi phí do đó có thể đáng kể và cần được hiểu rõ. Cách phát sinh chi phí khác nhau tùy theo cách sử dụng compute, storage và tài nguyên khác trên cloud, đòi hỏi quản lý chi phí khác so với hạ tầng on-premises có năng lực cố định.

AWS cung cấp nhiều cơ chế hiệu quả để tận dụng tối đa scale và elasticity mà cloud cung cấp, đồng thời đảm bảo bạn có thể hiểu và quản lý chi phí. Với các nguyên tắc hướng dẫn như trong The Frugal Architect, các công cụ và framework AWS giúp xây dựng kiến trúc hiệu quả, linh hoạt và mạnh mẽ để hỗ trợ HPC workloads.

Hãy xem xét [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected), cung cấp một pillar riêng về [cost-optimization](https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html) cùng các non-functional key khác như security, reliability, và sustainability.

---

#### Về tác giả

> **Alex Kimber**
>
> Alex Kimber là Principal Solutions Architect tại AWS Global Financial Services, với hơn 20 năm kinh nghiệm trong việc xây dựng và vận hành các nền tảng tính toán lưới hiệu suất cao (high performance grid computing platforms) tại các ngân hàng đầu tư.