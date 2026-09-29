# BÁO CÁO THỰC HÀNH AN TOÀN HỆ THỐNG THÔNG TIN
## BÀI THỰC HÀNH 4: KHẢO SÁT VÀ ĐÁNH GIÁ BỀ MẶT MẠNG BẰNG NMAP

---

### 1. THÔNG TIN SINH VIÊN
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên (MSSV):** 1150080083
- **Mã lớp học phần:** 11DHCNPM1
- **Tên bài thực hành:** LAB 4 - Khảo sát và đánh giá bề mặt mạng bằng Nmap

---

### 2. PHIÊN BẢN MÔI TRƯỜNG THỰC HÀNH
- **Hệ điều hành máy thật (Host):** Windows 11 Home 64-bit.
- **Nền tảng ảo hóa:** VMware® Workstation Pro 26H1u1 (Version: 26.0.1).
- **Máy quét (Scanner VM):** Kali Linux.
- **Máy đích kiểm thử (Target VM):** Metasploitable 2.

---

### 3. CÁCH THỨC DỰNG MÔI TRƯỜNG
1. **Thiết lập mạng nội bộ (Host-Only):**
   - Sử dụng card mạng ảo `VMnet1` của VMware ở chế độ **Host-only** để cách ly an toàn hoàn toàn với mạng bên ngoài.
   - Cấu hình dải mạng nội bộ: `192.168.56.0/24` (Subnet mask: `255.255.255.0`).
   - Kích hoạt dịch vụ DHCP trên `VMnet1` để tự động cấp phát IP cho các máy ảo trong bài lab.
2. **Cấu hình máy ảo:**
   - **Máy Kali Linux:** Gán Network Adapter vào `Custom: VMnet1 (Host-only)`. Địa chỉ IP nhận được: `192.168.56.1`.
   - **Máy Metasploitable 2:** Gán Network Adapter vào `Custom: VMnet1 (Host-only)`. Không sử dụng Bridged hay NAT. Địa chỉ IP nhận được: `192.168.56.10`.
3. **Sao lưu môi trường (Snapshot):**
   - Đã tạo Snapshot mang tên `Before-LAB4` trên cả hai máy ảo trước khi bắt đầu rà soát mạng để dễ dàng khôi phục trạng thái.

---



