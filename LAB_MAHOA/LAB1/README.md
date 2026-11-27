# LAB 1 – MÃ HÓA ĐỐI XỨNG CỔ ĐIỂN

**Họ và tên:** Đinh Thị Thảo An  
**MSSV:** 1150080083  
**Học phần:** An toàn và Bảo mật thông tin

## 1. Giới thiệu

Bài thực hành xây dựng chương trình minh họa sáu thuật toán mã hóa đối xứng cổ điển gồm **Caesar, Vigenère, Rail Fence, Playfair, Transposition và Autokey** bằng Java. Ứng dụng sử dụng **Java Swing** để nhập bản rõ, khóa, thực hiện mã hóa/giải mã và đọc/ghi tệp văn bản. Chương trình còn có giao diện tổng hợp, chức năng phân tích tấn công mật mã cổ điển và kết nối **Microsoft SQL Server** để lưu, xem lịch sử thao tác.

## 2. Công nghệ sử dụng

- Windows 11 (64-bit)
- OpenJDK Temurin 17
- Apache Maven 3.9.13
- Apache NetBeans IDE 31 và Java Swing
- Java (cài đặt thuật toán mã hóa cổ điển, xử lý tệp văn bản)
- Microsoft SQL Server và SQL Server Management Studio (SSMS)
- Microsoft JDBC Driver `mssql-jdbc` phiên bản `12.8.1.jre11`

## 3. Nội dung thực hành

| Bài | Nội dung | Thành phần chính |
|---|---|---|
| 1.1 | Mã hóa và giải mã Caesar | `CaesarCipher`, `frm_Caesar` |
| 1.2 | Mã hóa và giải mã Vigenère | `VigenereCipher`, `frm_Vigenere` |
| 1.3 | Mã hóa và giải mã Rail Fence | `RailFenceCipher`, `frm_RailFence` |
| 1.4 | Mã hóa và giải mã Playfair; hiển thị ma trận khóa | `PlayfairCipher`, `frm_Playfair` |
| 1.5 | Mã hóa và giải mã Transposition | `TranspositionCipher`, `frm_Transposition` |
| 1.6 | Mã hóa và giải mã Autokey | `AutokeyCipher`, `frm_Autokey` |
| Nâng cao 01 | Giao diện tổng hợp sáu thuật toán, lưu lịch sử thao tác | `CipherTongHop`, `frm_TongHop`, `HistoryDao` |
| Nâng cao 02 | Vét cạn Caesar, phân tích tần suất và known plaintext Vigenère | `AttackDemos`, `frm_TanCong` |
| Tích hợp | Menu chính, kiểm tra kết nối SQL Server, xem lịch sử | `frm_Menu`, `frm_KetNoiSQL`, `frm_LichSu`, `DbConfig` |

**Project Maven:** `LAB1_MaHoaCoDien`  
**Package:** `week_01`  
**Lớp chạy chính:** `week_01.frm_Menu`

## 4. Hướng dẫn chạy

### 4.1. Chạy chương trình Java trong NetBeans

1. Mở NetBeans → **File → Open Project** → chọn thư mục `LAB1_MaHoaCoDien` (thư mục chứa `pom.xml`).
2. Đảm bảo Maven đã tải dependency `mssql-jdbc`.
3. Nhấp phải project → **Clean and Build** (`Shift + F11`), kiểm tra `BUILD SUCCESS`.
4. Để chạy riêng một giao diện, nhấp phải file `frm_*.java` → **Run File** (`Shift + F6`).
5. Để chạy toàn bộ chương trình, nhấp phải project → **Run** (`F6`). Giao diện `frm_Menu` xuất hiện và có thể mở các chức năng tương ứng.

### 4.2. Kết nối SQL Server và xem lịch sử

1. Khởi động dịch vụ SQL Server; bảo đảm TCP/IP đã bật và cổng được cấu hình phù hợp (môi trường thực hành sử dụng `14333`).
2. Trong SSMS, chạy `sql/01_Tao_CSDL.sql` để tạo database và bảng lịch sử nếu chưa có.
3. Cấu hình tài khoản SQL Server có quyền `SELECT`, `INSERT`, `DELETE` trên bảng `dbo.history`. Tài khoản thực hành: `lab1_user`; **không lưu mật khẩu vào mã nguồn hoặc GitHub**.
4. Database: `LAB1_MaHoaCoDien`; bảng lưu lịch sử: `dbo.history`.
5. Từ `frm_Menu`, chọn **Kết nối SQL Server** → nhập Server, Port, Database, User và Password → **Test Connection**.
6. Quay lại chương trình tổng hợp, thực hiện mã hóa/giải mã để ghi lịch sử. Mở **Xem lịch sử** (`frm_LichSu`) và nhấn **Tải lại** để xem bản ghi.
7. Trong SSMS, chạy `sql/02_TruyVan_LichSu.sql` để xem 20 thao tác mới nhất, đếm bản ghi và thống kê theo thuật toán.

**Lưu ý:** Thông tin kết nối được nhập khi ứng dụng đang chạy. Khi đóng hẳn chương trình rồi mở lại, cần kết nối SQL Server lại trước khi ghi lịch sử.

## 5. Kết quả thực hành và kiểm thử

### 5.1. Sáu thuật toán mã hóa

| Bài | Plaintext | Key | Ciphertext đúng | Kết quả |
|---|---|---|---|---|
| 1.1 Caesar | `HELLO` | `3` | `KHOOR` | **PASS** |
| 1.2 Vigenère | `HELLO` | `KEY` | `RIJVS` | **PASS** |
| 1.3 Rail Fence | `HELLO WORLD` | `3` | `HOREL OLLWD` | **PASS** |
| 1.4 Playfair | `HELLOWORLD` | `KEYWORD` | `GYIZSCOKCFBU` | **PASS** |
| 1.5 Transposition | `BAOMAT` | `2,3,1` | `AAOTBM` | **PASS** |
| 1.6 Autokey | `HELLO` | `KEY` | `RIJSS` | **PASS** |

### 5.2. Chức năng nâng cao và tích hợp

| Chức năng | Nội dung kiểm thử | Kết quả ghi nhận |
|---|---|---|
| Project Maven | Clean and Build toàn bộ chương trình | **PASS** |
| Giao diện tổng hợp | Chọn và kiểm thử sáu thuật toán | **PASS** |
| Kết nối SQL Server | `frm_KetNoiSQL` → Test Connection | **PASS** |
| Lịch sử thao tác | Ghi và đọc dữ liệu từ `dbo.history` | **PASS** |
| Brute Force Caesar | Bản mã `KHOOR` → thử 26 khóa, tìm `k = 3`, `HELLO` | **PASS** |
| Frequency Analysis | `PHHW PH DIWHU WKH WRJD SDUWB` → H và W cùng chiếm 21,7% | **PASS** |
| Known Plaintext (Vigenère) | `HELLO` / `RIJVS` → suy ra `KEYKE` | **PASS** |
| Menu chính | Run Project (`F6`), kiểm tra 9 nút mở đúng form | **PASS** |

