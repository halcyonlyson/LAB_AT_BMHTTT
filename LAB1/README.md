# LAB 1: BẮT GÓI TIN TELNET - SSH
**Môn:** Thực hành An toàn Hệ thống thông tin

---

## 1. Thông tin sinh viên
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 115008083
- **Lớp:** 11CNPM1

---

## 2. Tên bài Lab
- **Lab 1: Examining SSH & Telnet in Wireshark (Bắt và phân tích gói tin Telnet - SSH)**

---

## 3. Nội dung đã thực hiện
- Thiết lập mô hình mạng gồm 3 máy (Server, Client, Attacker/Wireshark) trong cùng mạng LAN ảo.
- Tạo tài khoản người dùng thử nghiệm trên Server.
- Cấu hình và kích hoạt dịch vụ Telnet Server:
  - Sử dụng PuTTY/Terminal từ Client kết nối Telnet tới Server và thực thi lệnh.
  - Sử dụng Wireshark bắt gói tin qua cổng 23, phân tích luồng TCP Stream và trích xuất thông tin đăng nhập (username/password dạng plaintext).
  - Thử nghiệm đổi mật khẩu phức tạp hơn và quan sát kết quả bắt gói.
- Cấu hình và kích hoạt dịch vụ SSH Server:
  - Kết nối SSH từ Client tới Server qua cổng 22 và kiểm tra host-key fingerprint.
  - Sử dụng Wireshark bắt gói tin và phân tích gói SSH (dữ liệu payload bị mã hóa).
- Trả lời đầy đủ 11 câu hỏi lý thuyết và phân tích chuyên sâu trong báo cáo.

---

## 4. Kết quả thực hiện
- **Telnet:** Dữ liệu, lệnh thực thi và thông tin tài khoản (username/password) truyền ở dạng rõ (plaintext), dễ dàng bị đọc được khi dùng Wireshark bắt gói qua `tcp.port == 23`. Mật khẩu dù dài hay phức tạp cũng đều bị lộ.
- **SSH:** Toàn bộ payload trao đổi giữa Client và Server đều được mã hóa. Wireshark chỉ nhìn thấy metadata (IP nguồn/đích, cổng 22, handshake, kích thước gói) chứ không thể đọc được nội dung plaintext.
- **File đính kèm:**
  - File báo cáo chi tiết: `Lab1_11CNPM1_1150080083_DinhThiThaoAn.docx`
 
