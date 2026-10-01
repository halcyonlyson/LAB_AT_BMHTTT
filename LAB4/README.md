# BÁO CÁO THỰC HÀNH AN TOÀN HỆ THỐNG THÔNG TIN
## BÀI THỰC HÀNH 4: KHẢO SÁT VÀ ĐÁNH GIÁ BỀ MẶT MẠNG BẰNG NMAP

---

### 1. THÔNG TIN SINH VIÊN
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 1150080083
- **Mã lớp học phần:** 11DHCNPM1
- **Tên bài thực hành:** LAB 4 - Khảo sát và đánh giá bề mặt mạng bằng Nmap

---

### 2. PHIÊN BẢN MÔI TRƯỜNG THỰC HÀNH
- **Hệ điều hành máy thật (Host):** Windows 11 Home 64-bit.
- **Nền tảng ảo hóa:** VMware Workstation Pro 26H1u1 (Version 26.0.1).
- **Mô hình mạng:** Host-Only (`VMnet1`), dải mạng `192.168.56.0/24`.
- **Máy Host / VMware VMnet1:** `192.168.56.1`.
- **Máy quét (Scanner VM):** Kali Linux, IP `192.168.56.128`.
- **Công cụ quét:** Nmap 7.99.
- **Máy đích kiểm thử:** Metasploitable 2, IP `192.168.56.129`.
- **Máy đích đối chiếu:** Windows 11 x64 VM, IP `192.168.56.130`.
- **Dịch vụ thử nghiệm Hardening:** Python 3.14.7 HTTP Server trên TCP/8080.

---

### 3. CÁCH THỨC DỰNG MÔI TRƯỜNG

1. **Thiết lập mạng nội bộ (Host-Only):**
   - Sử dụng `VMnet1` của VMware ở chế độ **Host-only** để tạo mạng riêng phục vụ bài lab.
   - Dải mạng: `192.168.56.0/24` (Subnet mask `255.255.255.0`).
   - DHCP trên `VMnet1` được bật để cấp phát địa chỉ IP cho các máy ảo.

2. **Cấu hình các máy ảo:**
   - **Kali Linux:** Network Adapter đặt vào `Custom: VMnet1 (Host-only)`, IP `192.168.56.128`.
   - **Metasploitable 2:** Network Adapter đặt vào `Custom: VMnet1 (Host-only)`, IP `192.168.56.129`.
   - **Windows 11 VM:** Network Adapter đặt vào `Custom: VMnet1 (Host-only)`, IP `192.168.56.130`.
   - Không sử dụng Bridged cho các máy đích trong quá trình thực hành.

3. **Kiểm tra kết nối:**
   - Kiểm tra IP bằng `ip -br addr` trên Kali và `ifconfig` trên Metasploitable 2.
   - Từ Kali chạy `ping -c 4 192.168.56.129`; kết quả nhận đủ 4/4 gói tin, 0% packet loss.

---

### 4. CÁC TÌNH HUỐNG ĐÃ THỰC HIỆN VÀ KẾT QUẢ

| STT | Kịch bản / Tình huống thực hiện | Câu lệnh / Nội dung chính | Kết quả |
| :---: | :--- | :--- | :---: |
| 1 | Xác thực IP và kiểm tra kết nối | `ip -br addr`, `ifconfig`, `ping -c 4 192.168.56.129` | **PASS** |
| 2 | Host Discovery | `sudo nmap -sn 192.168.56.0/24` | **PASS** |
| 3 | Khảo sát TCP Connect / SYN | `nmap -sT 192.168.56.129`, `sudo nmap -sS 192.168.56.129` | **PASS** |
| 4 | FIN / Xmas / NULL / ACK Scan | `sudo nmap -sF`, `-sX`, `-sN`, `-sA` trên `192.168.56.129` | **PASS** |
| 5 | UDP Scan có kiểm soát | `sudo nmap -sU --top-ports 20 192.168.56.129` | **PASS** |
| 6 | Nhận diện dịch vụ | `sudo nmap -sV 192.168.56.129` | **PASS** |
| 7 | Nhận diện hệ điều hành và Aggressive Scan | `sudo nmap -O 192.168.56.129`, `sudo nmap -A 192.168.56.129` | **PASS** |
| 8 | NSE SMB | `smb-os-discovery`, `smb-vuln-ms17-010` trên TCP/445 | **PASS** |
| 9 | Xuất kết quả | `-oN`, `-oX`, `-oG` và `xsltproc` | **PASS** |
| 10 | Before/After Hardening trên Windows VM | HTTP TCP/8080: `open` trước hardening → `filtered` sau hardening | **PASS** |

