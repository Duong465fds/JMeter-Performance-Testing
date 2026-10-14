# Báo cáo thực hành kiểm thử hiệu năng bằng Apache JMeter

- **Sinh viên:** Duong465fds
- **Chủ đề:** Làm quen và thực hành kiểm thử tải bằng Apache JMeter
- **Tài liệu tham khảo:** [Repository mẫu quocbinh93/JMeter](https://github.com/quocbinh93/JMeter)
- **Tài liệu chính thức:** [Apache JMeter – Getting Started](https://jmeter.apache.org/usermanual/get-started.html)
- **Trang dự án:** [Apache JMeter](https://jmeter.apache.org/)

> **Quan trọng:** Hãy thực hiện bài test trên máy của bạn, chụp ảnh màn hình kết quả thật và thay các vị trí `[Chèn ảnh ...]` bên dưới. Không nộp báo cáo với ảnh giả hoặc kết quả chưa chạy.

## 1. Mục tiêu

- Tìm hiểu công cụ Apache JMeter và khái niệm kiểm thử tải (load testing).
- Tạo một Test Plan với Thread Group và HTTP Request.
- Chạy thử các request đến API công khai phục vụ kiểm thử.
- Đọc kết quả qua Summary Report và View Results Tree.
- Lưu Test Plan và ảnh minh họa lên GitHub.

## 2. Công cụ và môi trường

- Apache JMeter.
- Java phiên bản được hỗ trợ bởi bản JMeter đang sử dụng.
- API thực hành: `https://jsonplaceholder.typicode.com/`
- Các thành phần JMeter: Test Plan, Thread Group, HTTP Request, Summary Report, View Results Tree.

## 3. Chuẩn bị môi trường

1. Cài đặt Java phù hợp với phiên bản JMeter. Kiểm tra bằng lệnh `java -version`.
2. Tải bản phát hành JMeter từ trang chính thức: https://jmeter.apache.org/download_jmeter.cgi
3. Giải nén JMeter vào thư mục thuận tiện.
4. Trên Windows, mở thư mục `bin` và chạy `jmeter.bat`.
5. Chụp ảnh màn hình giao diện JMeter và kết quả kiểm tra Java.

[Chèn ảnh 1: Phiên bản Java và giao diện Apache JMeter]

## 4. Tạo Test Plan kiểm thử tải HTTP

### 4.1. Cấu hình Thread Group

1. Tạo Test Plan mới.
2. Nhấn chuột phải vào Test Plan → Add → Threads (Users) → Thread Group.
3. Thiết lập bài test nhỏ để thực hành:
   - Number of Threads (users): `5`
   - Ramp-up period (seconds): `5`
   - Loop Count: `2`
4. Các thông số trên tạo tối đa 10 lần thực thi sampler nếu mỗi thread chạy một vòng lặp có một sampler.

[Chèn ảnh 2: Cấu hình Thread Group]

### 4.2. Thêm HTTP Request

1. Nhấn chuột phải vào Thread Group → Add → Sampler → HTTP Request.
2. Cấu hình:
   - Protocol: `https`
   - Server Name or IP: `jsonplaceholder.typicode.com`
   - Method: `GET`
   - Path: `/posts/1`
3. Có thể để các trường khác theo mặc định.

[Chèn ảnh 3: Cấu hình HTTP Request GET /posts/1]

### 4.3. Thêm listener xem kết quả

Thêm hai listener vào Thread Group:
- Add → Listener → View Results Tree
- Add → Listener → Summary Report

Nhấn **Start** để chạy. Kiểm tra kết quả trong các listener sau khi chạy xong.

[Chèn ảnh 4: View Results Tree có phản hồi thành công]
[Chèn ảnh 5: Summary Report sau khi chạy]

## 5. Kết quả kiểm thử và phân tích

Ghi lại số liệu thực tế từ Summary Report:

| Chỉ số | Kết quả thực tế |
|---|---|
| Số mẫu (Samples) | Điền từ Summary Report |
| Average (thời gian phản hồi trung bình) | Điền từ Summary Report |
| Min (thời gian phản hồi nhỏ nhất) | Điền từ Summary Report |
| Max (thời gian phản hồi lớn nhất) | Điền từ Summary Report |
| Error % (tỷ lệ lỗi) | Điền từ Summary Report |
| Throughput (thông lượng) | Điền từ Summary Report |

**Nhận xét:** Dựa trên kết quả thực tế, nhận xét số lượng request, thời gian phản hồi và tỷ lệ lỗi. Thời gian phản hồi có thể thay đổi theo mạng, máy tính, thời điểm chạy và tình trạng máy chủ; không nên kết luận về hiệu năng tổng thể của hệ thống chỉ từ một lần chạy nhỏ.

## 6. Lưu Test Plan và chạy ở chế độ dòng lệnh (tùy chọn)

Lưu Test Plan với tên `jmeter-test-plan.jmx` trong thư mục `test-plans/`.

Để chạy bài test ở chế độ không giao diện (CLI), từ thư mục `bin` chạy lệnh tương tự sau (điều chỉnh đường dẫn nếu cần):

```bash
jmeter -n -t "C:\duong-dan\test-plans\jmeter-test-plan.jmx" -l "C:\duong-dan\results\results.jtl" -e -o "C:\duong-dan\results\html-report"
```

Thư mục đầu ra `html-report` cần chưa tồn tại hoặc đang trống. Với bài thực hành tải, Apache khuyến nghị chạy bằng CLI thay vì GUI để giảm ảnh hưởng của giao diện lên kết quả. Chỉ thử tải trên hệ thống bạn sở hữu hoặc được cho phép kiểm thử; không tạo tải lớn lên dịch vụ công cộng.

[Chèn ảnh 6: Báo cáo HTML được tạo sau khi chạy CLI, nếu thực hiện]

## 7. Cấu trúc repository đề xuất

```text
JMeter-Performance-Testing/
├── README.md
├── test-plans/
│   └── jmeter-test-plan.jmx
├── screenshots/
│   ├── 01-java-jmeter.png
│   ├── 02-thread-group.png
│   ├── 03-http-request.png
│   ├── 04-view-results-tree.png
│   └── 05-summary-report.png
└── results/
    └── README.md
```

Không bắt buộc phải commit các file kết quả lớn. Nếu đưa kết quả vào repository, hãy loại bỏ thông tin nhạy cảm và chỉ sử dụng dữ liệu không chứa thông tin cá nhân.

## 8. Kết luận

Qua bài thực hành, sinh viên làm quen với việc xây dựng Test Plan trong Apache JMeter, cấu hình số người dùng mô phỏng, gửi HTTP request và đọc số liệu trong Summary Report. Các chỉ số giúp quan sát phản hồi của dịch vụ trong điều kiện thử nghiệm đã cấu hình. Muốn đánh giá đáng tin cậy hơn cần thiết kế nhiều kịch bản, tăng tải có kiểm soát, lặp lại phép đo và phân tích kết quả.

## 9. Tài liệu tham khảo

1. [quocbinh93/JMeter – repository tham khảo](https://github.com/quocbinh93/JMeter)
2. [Apache JMeter – Getting Started](https://jmeter.apache.org/usermanual/get-started.html)
3. [Apache JMeter – User Manual](https://jmeter.apache.org/usermanual/)
4. [Apache JMeter – trang tải chính thức](https://jmeter.apache.org/download_jmeter.cgi)
5. [Apache JMeter – repository chính thức](https://github.com/apache/jmeter)

## 10. Checklist trước khi nộp

- [ ] Đã chạy Test Plan thực tế.
- [ ] Đã cập nhật bảng kết quả bằng số liệu của lần chạy.
- [ ] Đã chèn ảnh chụp màn hình thật vào thư mục `screenshots/`.
- [ ] Đã lưu file `.jmx`.
- [ ] Đã đổi tên tài liệu này thành `README.md`.
- [ ] Đã commit và push lên GitHub.
- [ ] Đã mở link repository ở chế độ đăng xuất/ẩn danh để kiểm tra quyền xem.
