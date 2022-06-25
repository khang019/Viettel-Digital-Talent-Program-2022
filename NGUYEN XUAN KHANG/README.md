# Final
# LOGGING CENTRALIZED ARCHITECTURES (CÁC MÔ HÌNH CENTRALIZED LOGGING)
## I. Centralized Logging
### 1. Khái niệm
Centralized Logging là một giải pháp về logging được thiết kế để thu thập log từ nhiều server và tổng hợp dữ liệu. Sau đó, hệ thống Centralized Logging sẽ trình bày dữ liệu tổng hợp trên một bảng điều khiển trung tâm.
Mục đích của Centralized Logging là tự động hóa quy trình quản lý logging thủ công, giảm thời gian và công sức khi phải duy trì một kho dữ liệu log khổng lồ.
### 2. Vai trò 
- Đơn giản hóa quá trình quản lý log.
- Tự động phát hiện lỗi.
- Tiết kiệm thời gian để giám sát.
- Tính bảo mật cao.
## II. Centralized Logging Architectures

Xây dựng một hệ thống Centralized Logging bao hàm 4 phần chính bao gồm: Thu thập Logs, Vận chuyển, Lưu trữ và Phân tích. 
### 1. Thu thập logs (Logs collection)
Các ứng dụng sẽ tạo ra logs theo nhiều cách khác nhau. Ví dụ như một ứng dụng web điển hình trên Linux sẽ tạo ra một lượng lớn logs trong tệp /var/log và cũng sẽ có một vài ứng dụng lưu trữ logs trong những vị trí riêng biệt.

Vì vậy việc thu thập các logs từ các ứng dụng hoặc server khác nhau là một bài toán khó. Chúng ta có thể sử dụng Replication Approach (Phương pháp tiếp cận nhân bản)

Trong Replication Approach, các tệp được sao chép đến một máy chủ trung tâm theo một lịch trình cố định. Chúng ta sẽ thiết lập một công việc cron sẽ sao chép các tệp trên máy chủ Linux sang máy chủ trung tâm. Tuy nhiên khi xảy ra sự cố người dùng sẽ phải đợi để các logs có thể được sao chép qua máy chủ trung tâm.

Replication approach sẽ tốt cho việc phân tích, nếu bạn cần phân tích dữ liệu nhật ký ngoại tuyến để tính toán số liệu hoặc công việc liên quan đến hàng loạt khác, thì Replication approach có thể phù hợp.
### 2. Vận chuyển (Transport)
Nếu bạn có nhiều máy chủ đang chạy thì dữ liệu logs có thể tích lũy một cách nhanh chóng. Vì vậy cần có một cách hiệu quả và đáng tin cậy để vận chuyển dữ liệu này đến máy chủ trung tâm và đảm bảo dữ liệu không bị mất.

Có nhiều framework có sẵn để vận chuyển dữ liệu logs. Một cách là plug trực tiếp các input soures và framework có thể bắt đầu thu thập logs. Một cách khác là gửi dữ liệu logs qua API, các application code được tạo ra để log trực tiếp vào các nguồn này, cách làm làm giảm độ trễ và cải thiện độ tin cậy.

Nếu dùng cách 1, chúng ta có thể sử dụng:
- Logstash - Trình thu thập logs nguồn mở, được viết bằng Ruby
- Flume - Bộ thu thập logs nguồn mở, được viết bằng Java
- Fluentd - Mã nguồn mở, được viết bằng Ruby
Các framework này cung cấp các input soures nhưng cũng hỗ trợ các tệp gắn đuôi nguyên bản và vận chuyển chúng một cách đáng tin cậy. Các framework này phù hợp các ứng dụng tổng quát.

Ghi dữ liệu logs qua các API là cách phổ biến hơn để ghi dữ liệu vào mày chủ trung tâm, đây là những framewwork có thể được sử dụng.
- Scribe - Phần mềm nguồn mở của Facebook, được viết bằng C ++
- nsq - Mã nguồn mở, viết bằng Go
- Kafka - Phần mềm nguồn mở được sử dụng nhiều bởi Apache, được viết bằng Java
