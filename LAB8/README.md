# LAB 8 – Local DNS Attack với pfSense

## 1. Thông tin sinh viên
- **Họ và tên:** Đinh Thị Thảo An
- **Mã số sinh viên:** 1150080083
- **Lớp:** 11DHCNPM1
- **Môn học:** An toàn hệ thống thông tin

## 2. Tên bài Lab
**LAB 8: Local DNS Attack – DNS Spoofing và Cache Poisoning trong mạng ảo cô lập**

## 3. Nội dung đã thực hiện
- Kế thừa mô hình mạng pfSense trên VMware Workstation, bổ sung mạng **DNSLAB (VMnet7)** với dải địa chỉ `10.9.0.0/24` và interface pfSense `10.9.0.1/24`.
- Thiết lập firewall rules để cô lập DNSLAB, giới hạn kết nối DNS đến AUTH-DNS và HTTP đến DMZ-WEB, bảo vệ mạng LAN và MGMT.
- Cấu hình **DNS-SERVER** (`10.9.0.10`), **VICTIM** (`10.9.0.100`), **Kali Linux** (`10.9.0.200`) và **APP-TEST** (`172.16.6.20`); tận dụng DMZ-WEB (`172.16.6.10`) từ LAB trước.
- Cài đặt BIND9, cấu hình zone thuận, zone nghịch và kiểm tra phân giải tên miền bằng dig, resolvectl.
- Chuẩn bị Python, Scapy, Wireshark và tcpdump trên Kali; triển khai dịch vụ AUTH-DNS mô phỏng trên APP-TEST.
- Minh họa cơ chế ưu tiên phân giải tên miền qua file `/etc/hosts`; thu thập gói DNS hợp lệ bằng tcpdump và phân tích file PCAP bằng Wireshark.
- Thực hiện các bước khôi phục file hosts, xóa cache DNS, kiểm tra cấu hình bảo vệ và tổng hợp nội dung báo cáo cùng 10 câu hỏi phân tích.

## 4. Kết quả thực hiện
- Đã cấu hình mô hình DNSLAB và địa chỉ IP cho các máy ảo; kết quả kiểm tra ICMP từ Kali phù hợp với chính sách cô lập mạng đã thiết lập.
- Đã cấu hình BIND9 thành công cho zone nội bộ: `www.lab9.test` và `portal.lab9.test` trả về `172.16.6.10`; các truy vấn PTR trả về đúng tên miền sau khi sửa tên reverse zone.
- AUTH-DNS trên APP-TEST đã phản hồi truy vấn trực tiếp `www.external.lab9.test` với IP `172.16.6.10`. Tuy nhiên, truy vấn qua BIND9 vẫn trả về NXDOMAIN do vấn đề phân giải giữa zone cha và forward zone; baseline external chưa đạt yêu cầu.
- Đã minh họa cơ chế HOSTS file bằng tên miền `hosts-demo.test` và địa chỉ loopback `127.0.0.1`. Chưa thực hiện đầy đủ kịch bản chuyển hướng sang Kali theo yêu cầu Task 1.
- Đã phân tích cặp gói DNS Query và DNS Response hợp lệ bằng Wireshark; xác nhận tên miền `www.lab9.test` được phân giải về `172.16.6.10`. File PCAP được thu thập trên DNS-SERVER, không phải bắt trực tiếp trên Kali.
- Chưa hoàn thành thực nghiệm Task 2 (Direct DNS Spoofing), Task 3 (DNS Cache Poisoning) và kiểm thử phòng thủ sau Cache Poisoning; không đánh giá các kịch bản này là PASS.
- Đã khôi phục file hosts; các bước kiểm tra cache và hardening được thực hiện theo phạm vi DNS nội bộ. Chưa có minh chứng khôi phục sau Cache Poisoning.
- Do tận dụng môi trường máy ảo hiện có, sử dụng VMware Workstation và Ubuntu 26.04.1 LTS thay cho VirtualBox và Ubuntu 24.04 trong tài liệu. Chưa xác nhận cơ chế tương đương với thiết lập Promiscuous Mode của VirtualBox.
