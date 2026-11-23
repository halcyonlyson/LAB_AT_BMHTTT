# LAB 3 – MÃ HÓA KHÓA CÔNG KHAI

**Họ và tên:** Đinh Thị Thảo An  
**MSSV:** 1150080083  
**Học phần:** An toàn và Bảo mật thông tin

## 1. Giới thiệu

Bài thực hành xây dựng chương trình minh họa mật mã khóa công khai RSA, ECC (ECDH + HKDF + AES-GCM), hệ mã lai RSA + AES và chữ ký số ECDSA bằng Java. Ứng dụng sử dụng Java Swing để thao tác mã hóa, giải mã, ký và xác minh; đồng thời kết nối Microsoft SQL Server để ghi nhận và tra cứu lịch sử.

**Lưu ý:** Đây là chương trình phục vụ học tập. Chỉ sử dụng khóa thử nghiệm; không công khai khóa riêng, mật khẩu hoặc tệp chứa thông tin bí mật. Chức năng Save Keys trong hướng dẫn ghi khóa riêng dưới dạng Base64, **không phải mã hóa bảo vệ khóa riêng**.

## 2. Công nghệ sử dụng

- Windows 11 (64-bit)
- OpenJDK Temurin 17.0.16 (đã kiểm tra)
- Apache Maven 3.9.13 (đã kiểm tra)
- Apache NetBeans IDE và Java Swing
- Java Cryptography Architecture / Java Cryptography Extension (RSA, EC, ECDH, AES-GCM, ECDSA)
- Microsoft SQL Server và SQL Server Management Studio (SSMS)
- Microsoft JDBC Driver `mssql-jdbc` phiên bản `12.8.1.jre11` (theo `pom.xml` của tài liệu)

## 3. Nội dung thực hành

| Bài | Nội dung | Công nghệ |
|---|---|---|
| 3.1 | RSA Console – tạo khóa 2048/3072 bit, mã hóa/giải mã `HELLO RSA`, so sánh độ dài và thời gian | Java Console |
| 3.2 | RSA Swing – mã hóa/giải mã RSA-OAEP SHA-256 | Java Swing |
| 3.3 | ECC – ECDH + HKDF-SHA256 + AES-256-GCM; Save/Load Keys và thử khóa sai | Java Swing |
| 3.4 | Hệ mã lai RSA + AES – mã hóa văn bản trên 1.000 ký tự, phát hiện bản mã bị sửa | Java Swing |
| 3.5 | ECDSA – ký/xác minh thông điệp, thử thay đổi thông điệp hoặc khóa | Java Swing |
| Tích hợp | Menu chính, kết nối SQL Server và lưu/xem lịch sử `dbo.History` | JDBC, SQL Server |

Project Maven: `LAB3_MaHoaKhoaCongKhai`; package: `week_03`; lớp chạy chính: `week_03.frm_Menu`.

## 4. Hướng dẫn chạy

### 4.1. Chạy chương trình Java trong NetBeans

1. Mở NetBeans, chọn **File → Open Project** và mở thư mục `LAB3_MaHoaKhoaCongKhai` (chứa `pom.xml`).
2. Đảm bảo Maven đã tải dependency `mssql-jdbc`.
3. Nhấp phải project → **Clean and Build** (`Shift + F11`), kiểm tra `BUILD SUCCESS`.
4. Khi đang thực hiện từng bài, nhấp phải tệp form hoặc `RSADemo.java` → **Run File** (`Shift + F6`).
5. Sau khi hoàn thành `frm_Menu`, chọn **Run Project** (`F6`) để mở menu chính, rồi chọn chức năng muốn kiểm thử.

### 4.2. Kết nối SQL Server

1. Khởi động dịch vụ SQL Server; theo cấu hình tài liệu, bật TCP/IP và đặt cổng `14333`.
2. Trong SSMS, chạy lần lượt các script: `01_Tao_CSDL.sql`, `02_Tao_TaiKhoan_LAB.sql`.
3. Database: `LAB3_MaHoaKhoaCongKhai`; bảng lịch sử: `dbo.History`.
4. Từ `frm_Menu`, mở **Kết nối SQL Server**, nhập thông tin đăng nhập của máy thực hành và chọn **Test Connection**.
5. Mở **Xem lịch sử** (`frm_LichSu`), chọn **Tải lại** để xem bản ghi.
6. Chạy `03_KiemTra_LichSu.sql` trong SSMS để xem 30 dòng mới nhất và thống kê thao tác theo thuật toán.

**Bảo mật:** Không đưa mật khẩu SQL Server hoặc khóa riêng lên GitHub. Không chụp màn hình có thông tin bí mật. Khóa lưu bằng Save Keys chỉ dùng làm dữ liệu thử nghiệm và phải được giữ riêng, không commit.

## 5. Kết quả thực hành và kiểm thử
