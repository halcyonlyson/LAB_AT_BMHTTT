# LAB 6 – Xác thực Active Directory và chính sách truy cập trên pfSense

## 1. Thông tin sinh viên
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 1150080083
- **Lớp:** 11DHCNPM1
- **Môn học:** An toàn hệ thống thông tin

## 2. Tên bài Lab
**LAB 6: Xác thực Active Directory và chính sách truy cập trên pfSense**

## 3. Nội dung đã thực hiện
- Xây dựng mô hình mạng trên VMware Workstation với bốn vùng **WAN, MGMT, LAN, DMZ** và cấu hình các interface trên pfSense.
- Cài đặt Windows Server 2022, Active Directory Domain Services (AD DS), DNS và chuẩn bị tài khoản `sv_a`, `sv_b` cùng tài khoản dịch vụ LDAP.
- Cấu hình pfSense xác thực Active Directory qua LDAP; thiết lập Captive Portal trên LAN.
- Cấu hình hai máy trạm Windows 11 và Ubuntu Server chạy Nginx trong DMZ, mô phỏng các website bằng địa chỉ IP riêng.
- Tạo các **Firewall Alias** cho máy trạm, website và cổng HTTP/HTTPS; tạo lịch **LUNCH_WINDOW**, **WORK_HOURS** và **TEST_NOW**.
- Thực hiện các kịch bản Firewall: chặn JOB_SITE, chặn RESTRICTED_SITE, giới hạn SOCIAL_SITE theo giờ nghỉ, giới hạn HTTP/HTTPS theo giờ hành chính và cô lập DMZ khỏi LAN.
- Kiểm tra cấu hình, truy cập thử và phân tích Firewall Log theo các kịch bản trong báo cáo.

## 4. Kết quả thực hiện
- Đã thiết lập mô hình mạng và địa chỉ IP cho các máy ảo theo cấu trúc LAB 6.
- Ubuntu Server đã hoạt động với Nginx và các địa chỉ IP website mô phỏng; kiểm tra HTTP trả về **200 OK**.
- Đã cấu hình LDAP trên pfSense; báo cáo có hình ảnh xác thực thành công `sv_a`, `sv_b`, tuy nhiên bảng tổng kết vẫn ghi cần xác nhận đầy đủ cả hai tài khoản.
- Đã tạo Captive Portal, Firewall Alias, Schedule và các Firewall Rule phục vụ từng kịch bản.
- Đã ghi nhận log chặn truy cập ở các kịch bản kiểm thử. Riêng kịch bản SOCIAL_SITE theo lịch **TEST_NOW**, Client-B vẫn bị chặn nên chưa xác minh được cơ chế cho phép theo thời gian.
- Một số kết quả kiểm thử cuối (Captive Portal, JOB_SITE, RESTRICTED_SITE, WORK_HOURS) còn được ghi là **chưa xác minh đầy đủ** trong bảng tổng kết báo cáo; không xem là đã thành công hoàn toàn.

## 5. Tệp đính kèm
- Báo cáo thực hành LAB 6.
- File `config.xml` sao lưu cấu hình pfSense.

> **Lưu ý bảo mật:** File `config.xml` có thể chứa thông tin xác thực hoặc cấu hình nhạy cảm; chỉ nộp qua kênh được giảng viên chỉ định, không công khai lên kho mã nguồn.
