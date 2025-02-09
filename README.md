Đỗ Lê Việt Anh - BIT220014 - 22SE1

# Kiểm thử phi chức năng với JMeter
## Giới thiệu
Dự án này sử dụng Apache JMeter để đánh giá hiệu suất của một trang web thương mại điện tử thông qua kiểm thử tải (Load Testing) và kiểm thử khả năng chịu tải (Stress Testing).

## Hướng dẫn sử dụng
### 1. Cài đặt
- Yêu cầu: 
    - Apache JMeter
    - Java 8 hoặc mới hơn.
## Cài đặt Apache JMeter
### Bước 1: Tải và cài đặt Java
JMeter yêu cầu Java để chạy. Kiểm tra phiên bản Java:
```
java -version
```
Nếu chưa có, tài và cài đặt từ trang web chính của Java: https://www.java.com

### Bước 2: Tải và cài đặt Apache JMeter
- Truy cập website của JMeter: https://jmeter.apache.org/download_jmeter.cgi
- Tải phiên bản mới nhất.
- Giải nén và chạy JMeter bằng lệnh:
```
cd apache-jmeter/bin
./jmeter.sh   # Mac/Linux
jmeter.bat    # Windows
```

## Mô tả bài tập
### 1. Kiểm thử hiệu suất
- Mô phỏng 50 người dùng đồng thời truy cập trang web trong vòng 5 phút.
- Gửi yêu cầu HTTP đến trang chủ của website.
- Đo thời gian phản hồi và xác định bottleneck nếu có.
### 2. Kiểm thử tải
- Chạy kiểm thử với số lượng người dùng tăng dần từ 10 → 50.
- Ghi nhận thời gian phản hồi trung bình và tỷ lệ lỗi (Error Rate).
### 3. Kiểm thử khả năng chịu tải
- Tiếp tục tăng số người dùng lên 100 và xác định giới hạn chịu tải của hệ thống.
- Quan sát thời điểm hệ thống bắt đầu giảm hiệu suất đáng kể.

## Kết quả 
### 1. Kiểm thử hiệu suất
- Thời gian phản hồi:
    - Thời gian phản hồi trung bình: **36ms**
    - Dao động từ **2ms** đến **803ms**
    - Nhận xét: ⏳ Hệ thống có thời gian phản hồi tốt với tải thông thường, nhưng có một số yêu cầu chậm lên đến 803ms, có thể do giới hạn tài nguyên hoặc truy vấn chậm.
- Throughput (Yêu cầu xử lý mỗi giây): **1325 request/s**
    - Nhận xét: 📈 Hệ thống có khả năng xử lý yêu cầu cao khi tải ở mức vừa phải.
- Tỷ lệ lỗi: **0%**
    - Nhận xét: ✅ Không có lỗi nào xảy ra, cho thấy hệ thống ổn định với tải 50 users.
#### Kết luận: ✅ Không có lỗi nào xảy ra, cho thấy hệ thống ổn định với tải 50 users.
#### Đề xuất cải tiến:
- **Tối ưu hóa database** để giảm độ trễ truy vấn.
- **Sử dụng cache** để giảm tải cho backend.
- **Giám sát server** để đảm bảo tài nguyên không bị giới hạn.
### 2. Kiểm thử Tải
- Thời gian phản hồi:
    |Số người dùng   |   Thời gian phản hổi trung bình|Min(ms)   |Max(ms)   |Độ lệch chuẩn   |
    |---|---|---|---|---|
    | 10 |5ms|2ms   |432ms   |10.48   |
    | 30 |7ms|2ms   |3035ms   | 12.89  |
    | 50 |9ms|2ms   |3035ms   |   15.03|
    - 📌 Nhận xét: Khi số lượng người dùng tăng lên, thời gian phản hồi tăng từ **5ms (10 users) → 7ms (30 users) → 9ms (50 users)**. Điều này cho thấy hệ thống vẫn giữ được hiệu suất khá tốt, nhưng có một số yêu cầu mất nhiều thời gian hơn khi tải tăng lên.
- Throughput (Yêu cầu xử lý mỗi giây): 
    | Số người dùng  |Throughput(request/s)   | 
    |---|---|
    | 10  | 1658.18  |   
    |   30| 2417.50  |   
    |   50|   2943.78|   
    - 📌 Nhận xét: Throughput tăng dần khi số lượng người dùng tăng, từ **1658 req/sec (10 users) → 2943 req/sec (50 users)**. Điều này cho thấy hệ thống có khả năng mở rộng tốt.
- Tỷ lệ lỗi: Cả ba mức tải đều có **0% lỗi**, cho thấy hệ thống vẫn hoạt động ổ định dủ tăng số lượng người dùng
#### Kết luận:
- ✅ Hệ thống có hiệu suất tốt với mức tải từ 10 đến 50 users.
- ⚠️ Tuy nhiên, thời gian phản hồi tăng dần và có một số yêu cầu chậm hơn khi tải tăng cao.
#### Đề xuất cải tiến:
- **Tối ưu hóa cơ sở dữ liệu** để giảm độ trễ xử lý.
- **Tăng cường caching** để giảm tải backend.
- **Cân nhắc mở rộng tài nguyên** server để đảm bảo hiệu suất khi số lượng người dùng tiếp tục tăng.
### 3. Kiểm thử khả năng chịu Tải
- Thời gian phản hồi:
    - Thời gian phản hồi trung bình: **77ms**
    - Dao động từ **3ms** đến **437ms**
    - Nhận xét: ⏳ Khi tải tăng lên 100 users, thời gian phản hồi tăng gần gấp đôi, cho thấy dấu hiệu của quá tải.
- Throughput (Yêu cầu xử lý mỗi giây): **77 request/s**
    - Nhận xét: 📉 Throughput giảm mạnh khi tải tăng, cho thấy hệ thống bắt đầu bị giới hạn tài nguyên.
- Tỷ lệ lỗi: **0%**
    - Kết luận: ✅ Không có lỗi xảy ra, nhưng hiệu suất giảm khi tải tăng cao.
#### Kết luận: Hệ thống bắt đầu gặp giới hạn khi tăng tải lên 100 users. Throughput giảm và thời gian phản hồi tăng, cho thấy cần tối ưu thêm để duy trì hiệu suất.
#### Đề xuất cải tiến:
- **Nâng cấp tài nguyên** phần cứng hoặc cân nhắc mở rộng hệ thống.
- **Tối ưu hóa mã nguồn** để xử lý yêu cầu hiệu quả hơn.
- **Sử dụng load balancing** để chia tải giữa nhiều máy chủ.

## ❓ Câu hỏi thảo luận:
### 1. Tại sao kiểm thử phi chức năng lại quan trọng trong phần mềm?
- Đảm bảo hệ thống hoạt động ổn định dưới tải lớn.
- Xác định giới hạn chịu tải trước khi triển khai thực tế.
- Giúp tối ưu hiệu suất, tránh downtime
### 2. Các thông số quan trọng cần theo dõi trong kiểm thử hiệu suất là gì?
- Response Time (ms) – thời gian phản hồi trung bình.
- Throughput (requests/sec) – số yêu cầu xử lý mỗi giây.
- Error Rate (%) – tỷ lệ lỗi.
- CPU & Memory Usage – tài nguyên hệ thống.
### 3.Nếu hệ thống không đáp ứng yêu cầu hiệu suất, bạn sẽ đề xuất giải pháp gì?
- Tối ưu mã nguồn & database (caching, indexing).
- Tăng tài nguyên máy chủ (RAM, CPU).
- Dùng Load Balancer để phân tán tải.
- Dùng CDN để giảm tải trực tiếp lên server.

### Link ChatGPT: https://chatgpt.com/share/67a85f66-2e60-800c-9ff0-4398fe527269
