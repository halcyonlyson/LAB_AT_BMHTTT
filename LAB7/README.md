# LAB 7 – Bảo vệ truy cập Web với pfSense và Web Proxy

## 1. Thông tin sinh viên
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 1150080083
- **Lớp:** 11DHCNPM1
- **Môn học:** An toàn hệ thống thông tin

## 2. Tên bài Lab
**LAB 7: pfSense Web Protection – Kiểm soát truy cập và lọc nội dung Web**

## 3. Nội dung đã thực hiện
- Xây dựng lại mô hình mạng LAB 6 trên VMware Workstation với bốn vùng **WAN, MGMT, LAN, DMZ** và pfSense CE 2.7.2.
- Cấu hình Windows Server 2022 (DC01) cung cấp DNS cho các tên miền mô phỏng `lab7.test`; triển khai Nginx trên DMZ-WEB.
- Triển khai WEB-PROXY trên Ubuntu Server với địa chỉ IP `10.6.0.30`, sử dụng **Squid, E2Guardian và ClamAV**; cấu hình máy trạm sử dụng proxy qua cổng `8080`.
- Tạo Firewall Alias và Firewall Rules trên pfSense để chặn truy cập web trực tiếp từ Client và cho phép truy cập thông qua proxy.
- Cấu hình các chính sách Hard Block, Warning, Temporary Bypass 300 giây và Whitelist trên E2Guardian.
- Thiết lập Schedule `LAB7_ENT_60M` để kiểm soát truy cập website giải trí và trò chơi theo khung giờ 60 phút.
- Cấu hình quét nội dung tải xuống bằng ClamAV, giới hạn dung lượng phản hồi HTTP 100 MB bằng Squid và tùy biến trang Block của E2Guardian.
- Thực hiện các kịch bản kiểm thử, đối chiếu nhật ký pfSense, E2Guardian, Squid và ClamAV; tổng hợp nội dung báo cáo và câu hỏi phân tích.

## 4. Kết quả thực hiện
- Đã triển khai mô hình mạng, hệ thống DNS, Nginx và Web Proxy; website bình thường truy cập được qua proxy.
- Đã kiểm thử chức năng Hard Block đối với các website thuộc nhóm Geo-Sim, Job Search và Specific Game. Liên kết Acknowledge vẫn có thể hiển thị trên trang chặn cứng nhưng không mở khóa được website trong các lần kiểm thử đã xác nhận.
- Đã cấu hình nhóm Warning và Temporary Bypass; truy cập các website thuộc Whitelist thành công. Thời điểm hết hạn bypass vẫn cần xác minh đầy đủ.
- Đã xác nhận truy cập website Entertainment/Game trong khung giờ cho phép; kết quả kiểm thử ngoài khung giờ cần được đối chiếu thêm.
- Đã tùy biến trang Block và khôi phục hoạt động E2Guardian sau sự cố cấu hình HTML Template.
- Đã triển khai cấu hình ClamAV và giới hạn tải xuống. Tuy nhiên, chưa có đủ minh chứng xác nhận ClamAV phát hiện EICAR và kết quả phân biệt file 100 MB với 110 MB; không đánh giá hai kịch bản này là PASS hoàn toàn.
- Do hạn chế môi trường máy ảo, sử dụng một máy Client với hai địa chỉ IP `10.6.0.21` và `10.6.0.22` luân phiên thay cho hai máy Client độc lập. Không triển khai HTTPS Inspection (phần mở rộng).

