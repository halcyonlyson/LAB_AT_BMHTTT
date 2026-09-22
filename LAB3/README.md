# Báo cáo Lab 3: Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin

- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên (MSSV):** 1150080083
- **Mã lớp:** 11DHCNPM1

---

## 1. Phiên bản môi trường thực hành
- **Ảo hóa:** VMware Workstation Pro 26H1 (Chế độ mạng: Host-only)
- **Hệ điều hành máy ảo:** Windows 11 25H2 x64, OS build 26200.9445 (Bản cập nhật KB5124008)
- **Cơ chế bảo vệ (Endpoint Protection):** Microsoft Defender Antivirus (Real-time Protection & Tamper Protection: Enabled)
- **Môi trường dòng lệnh:** Windows PowerShell 5.1 (Run as administrator)
- **Phiên bản các công cụ:**
  - Python: `3.14.7`
  - Wireshark: `4.6.8 Stable` + Npcap
  - Microsoft Sysinternals Sysmon: `15.22` (Schema 4.90)
  - Microsoft Sysinternals Autoruns: `14.3`
  - Microsoft Sysinternals Process Explorer: `17.14`
- **Gói dữ liệu thực hành:** `LAB3_Threats_Assets.zip`
  - SHA-256: `96236f95ce59d0cc37f9b7ab8fbb04522f21870cd0b53aad6e52da5a23655439`

---

## 2. Cách dựng môi trường
1. **Khởi tạo VM:** Dựng máy ảo Windows 11 25H2 trên VMware Workstation Pro 26H1, cấu hình card mạng Host-only, cập nhật bản vá KB5124008 và tạo snapshot `LAB3_CLEAN_20260914`.
2. **Cấu trúc thư mục:** Khởi tạo thư mục gốc `C:\LAB3` gồm 4 thư mục con `Evidence`, `Tools`, `Downloads`, `Assets` và ghi nhận mốc thời gian bắt đầu.
3. **Chuẩn bị dữ liệu:** Đặt tệp `LAB3_Threats_Assets.zip` vào `C:\LAB3\Downloads`, đối chiếu mã hash SHA-256 với manifest gốc trước khi giải nén vào `C:\LAB3`.
4. **Cài đặt phần mềm:** Cài đặt Python 3.14.7 và Wireshark 4.6.8 qua `winget`. Tải gói chính thức của Sysmon, Autoruns, Process Explorer từ `download.sysinternals.com` và giải nén vào `C:\LAB3\Tools`.
5. **Thu thập Baseline:** Thực thi script PowerShell lấy baseline của hệ điều hành, Defender, Firewall, IP configuration và danh sách tiến trình trước khi thực hiện các tình huống.

---

## 3. Tóm tắt kết quả thực hiện các tình huống (PASS/FAIL)

| Tình huống | Tên tình huống | Mục tiêu chính | Kết quả |
| :---: | :--- | :--- | :---: |
| **TH1** | Baseline và Risk Register | Lập Risk Register (5 tài sản/nguy cơ) và phân loại đúng 5 nguồn mối đe dọa. | **PASS** |
| **TH2** | Mã độc (EICAR Test File) | Defender chặn và cách ly tệp EICAR theo thời gian thực; xuất hiện trong Protection History. | **PASS** |
| **TH3** | Tấn công mật khẩu & Keylogging | Ghi nhận Security Event ID 4624/4648 khi đăng nhập đúng và 4625 khi sai; đổi mật khẩu vô hiệu hóa credential cũ. | **PASS** |
| **TH4** | Backdoor, Persistence & Listener | Phát hiện Run value, Scheduled Task qua Sysmon/Autoruns; xác định tiến trình python.exe lắng nghe cổng 8080 cục bộ qua Process Explorer. | **PASS** |
| **TH5** | Sniffing, MITM & Spoofing | Wireshark capture được chuỗi plaintext trong URL HTTP loopback; so sánh được sự khác biệt về payload/metadata đối với luồng TLS 443. | **PASS** |
| **TH6** | DoS, DDoS & Mail Bombing | Chạy tải giới hạn trên localhost; phân tích các nguồn phân tán trong `ddos_sample.csv` và khối lượng bất thường trong `mailbomb_sample.csv`. | **PASS** |
| **TH7** | Social Engineering & Phishing | Nhận diện 5 chỉ dấu trong mẫu `phishing_email.txt`; phân loại đúng 6 case Social Engineering trong CSV. | **PASS** |
| **Cleanup** | Cô lập, Dọn dẹp & Phục hồi | Xóa Run key, Scheduled Task, kill listener 8080, xóa tài khoản lab; so sánh baseline Autoruns sạch; tính SHA-256 toàn bộ thư mục Evidence. | **PASS** |
