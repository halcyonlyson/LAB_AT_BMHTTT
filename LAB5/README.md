# LAB 5 – THIẾT LẬP MÔ HÌNH TƯỜNG LỬA pfSense

## 1. Thông tin sinh viên
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 1150080083
- **Lớp:** 11DHCNPM1
- **Môn học:** An toàn hệ thống thông tin

## 2. Tên bài Lab
**LAB 5: Thiết lập mô hình tường lửa pfSense**

## 3. Nội dung đã thực hiện
- Kiểm tra giá trị SHA-256 của bộ cài pfSense CE 2.7.2.
- Tạo mô hình mạng ảo trên VMware Workstation gồm WAN (Bridged), LAN (VMnet2 – 10.0.0.0/8) và DMZ (VMnet3 – 172.16.0.0/16).
- Cài đặt pfSense CE 2.7.2, gán giao diện WAN, LAN, DMZ và thiết lập địa chỉ IP.
- Cài đặt, cấu hình Windows Server 2022 với Active Directory Domain Services và DNS cho miền `lab3.test`.
- Truy cập giao diện quản trị pfSense WebGUI, kiểm tra trạng thái các interface và các Firewall Rule.
- Thiết lập quy tắc tường lửa nhằm chặn lưu lượng từ vùng DMZ truy cập mạng LAN.
- Tìm hiểu vai trò của NAT, Firewall Rule, DMZ, thứ tự xử lý rule, logging và các biện pháp hardening pfSense.

## 4. Kết quả thực hiện
- Kiểm tra SHA-256 của bộ cài pfSense cho kết quả khớp với giá trị trong tài liệu thực hành.
- Cài đặt và khởi động pfSense; cấu hình được ba giao diện WAN, LAN và DMZ.
- Kiểm tra kết nối Internet từ pfSense bằng `ping 8.8.8.8` thành công.
- Cấu hình Active Directory/DNS trên Windows Server 2022; kết quả kiểm tra DNS được thể hiện trong báo cáo.
- Truy cập được pfSense WebGUI và xem trạng thái các interface.
- Đã thiết lập rule **Block DMZ → LAN**. Báo cáo chưa cung cấp bằng chứng kiểm thử cuối cùng xác nhận lưu lượng DMZ → LAN bị chặn.
- Các cấu hình NAT/Port Forward và các kịch bản kiểm thử khác được nêu ở phần mục tiêu hoặc giải thích lý thuyết; báo cáo chưa thể hiện đầy đủ kết quả triển khai thực tế.

## 5. Tài liệu minh chứng
- `11DHCMPM1_LAB5_1150080083_DinhThiThaoAn.docx`: báo cáo thực hành, hình ảnh cấu hình và phần trả lời câu hỏi.


