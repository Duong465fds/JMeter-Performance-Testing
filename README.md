# Báo cáo thực hành kiểm thử hiệu năng bằng Apache JMeter

- **Sinh viên:** Duong465fds
- **Chủ đề:** Làm quen và thực hành kiểm thử tải bằng Apache JMeter
- **Tài liệu tham khảo:** [Repository mẫu quocbinh93/JMeter](https://github.com/quocbinh93/JMeter)
- **Tài liệu chính thức:** [Apache JMeter – Getting Started](https://jmeter.apache.org/usermanual/get-started.html)
- **Trang dự án:** [Apache JMeter](https://jmeter.apache.org/)

> **Quan trọng:** Hãy thực hiện bài test trên máy của bạn, chụp ảnh màn hình kết quả thật và thay các vị trí `[Chèn ảnh ...]` bên dưới. Không nộp báo cáo với ảnh giả hoặc kết quả chưa chạy.



**Mục tiêu:**
- Tạo và cấu hình Test Plan.
- Gửi nhiều HTTP Request đến API.
- Theo dõi kết quả phản hồi.
- Đo thời gian phản hồi và thông lượng.
- Đánh giá tỷ lệ lỗi của các request.

## 2. Công cụ sử dụng

| Thành phần | Thông tin |
|---|---|
| Công cụ kiểm thử | Apache JMeter 5.6.3 |
| API kiểm thử | JSONPlaceholder |
| URL | https://jsonplaceholder.typicode.com/posts/1 |
| HTTP Method | GET |
| Test Plan | JMeter API Performance Test |

## 3. Cấu hình Test Plan

Thread Group được cấu hình như sau:

| Thuộc tính | Giá trị |
|---|---:|
| Number of Threads (Users) | 5 |
| Ramp-up Period | 5 giây |
| Loop Count | 2 |
| Tổng số request dự kiến | 10 |

Công thức tính số request:

`5 users × 2 loops = 10 requests`

### 3.1. Cấu hình Thread Group

![Thread Group Configuration](screenshots/01-thread-group.png)

### 3.2. Cấu hình HTTP Request

| Thuộc tính | Giá trị |
|---|---|
| Protocol | HTTPS |
| Server Name | jsonplaceholder.typicode.com |
| Method | GET |
| Path | /posts/1 |

![HTTP Request Configuration](screenshots/02-http-request.png)

## 4. Theo dõi kết quả

JMeter sử dụng Listener **View Results Tree** để theo dõi từng request và kiểm tra phản hồi của API.

![View Results Tree](screenshots/03-view-results-tree.png)

## 5. Kết quả kiểm thử

Dữ liệu dưới đây được ghi nhận từ Summary Report của lần chạy JMeter thực tế.

| Chỉ số | Kết quả |
|---|---:|
| Samples | 10 |
| Average Response Time | 3211 ms |
| Minimum Response Time | 28 ms |
| Maximum Response Time | 8351 ms |
| Standard Deviation | 3330.32 ms |
| Error Rate | 0.00% |
| Throughput | 1.2 requests/sec |
| Received KB/sec | 1.54 |
| Sent KB/sec | 0.16 |
| Average Bytes | 1322.2 |

### 5.1. Summary Report

![JMeter Summary Report](screenshots/04-summary-report.png)

## 6. Phân tích kết quả

- **Samples = 10:** Có 10 request được ghi nhận, phù hợp với cấu hình 5 người dùng và 2 vòng lặp.
- **Average = 3211 ms:** Thời gian phản hồi trung bình trong lần chạy này khoảng 3,21 giây.
- **Min = 28 ms:** Request nhanh nhất phản hồi trong 28 ms.
- **Max = 8351 ms:** Request chậm nhất phản hồi trong khoảng 8,35 giây.
- **Error Rate = 0.00%:** Summary Report không ghi nhận request lỗi trong lần chạy này.
- **Throughput = 1.2 requests/sec:** Hệ thống xử lý trung bình khoảng 1,2 request mỗi giây trong lần kiểm thử.

Thời gian phản hồi có sự chênh lệch đáng kể giữa các request. Nguyên nhân có thể liên quan đến kết nối mạng, độ trễ của dịch vụ hoặc điều kiện thực hiện kiểm thử.

## 7. Kết luận

Bài thực hành đã hoàn thành việc tạo Test Plan, cấu hình Thread Group, gửi HTTP GET Request và sử dụng Listener để thu thập kết quả.

Trong lần chạy được ghi nhận, JMeter có 10 mẫu với tỷ lệ lỗi 0.00%. Tuy nhiên, thời gian phản hồi dao động khá lớn.

Do số lượng request còn nhỏ, kết quả chỉ phản ánh một lần kiểm thử cơ bản và chưa đủ để đánh giá khả năng chịu tải cao của API. Có thể tiếp tục thử nghiệm với số lượng người dùng lớn hơn và nhiều lần chạy để có đánh giá đầy đủ hơn.

## 8. Cấu trúc repository

```text
JMeter-Performance-Testing/
├── README.md
├── screenshots/
│   ├── 01-thread-group.png
│   ├── 02-http-request.png
│   ├── 03-view-results-tree.png
│   └── 04-summary-report.png
└── results/
```

## 9. Tài liệu tham khảo

- Apache JMeter Getting Started: https://jmeter.apache.org/usermanual/get-started.html
- Apache JMeter Downloads: https://jmeter.apache.org/download_jmeter.cgi
- Repository tham khảo: https://github.com/quocbinh93/JMeter
