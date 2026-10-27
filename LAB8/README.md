LAB 8 – Local DNS Attack: DNS Spoofing và Cache Poisoning
1. Thông tin sinh viên
- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 8
2. Môi trường thực hành
- VMware Workstation (môi trường sử dụng từ các LAB trước; điều chỉnh cấu hình mạng tương ứng với tài liệu VirtualBox)
- pfSense CE 2.7.2
- Ubuntu Server/Desktop 24.04
- Kali Linux
- BIND9, Wireshark, Scapy, tcpdump, dnsutils
- DNS-LAB: 10.9.0.0/24 (mạng ảo cô lập)
- LAN-DOMAIN: 10.6.0.0/24 (VMnet2)
- DMZ: 172.16.6.0/24 (VMnet3)
- pfSense DNSLAB: 10.9.0.1/24
- DNS-SERVER: 10.9.0.10/24
- VICTIM: 10.9.0.100/24
- ATTACKER (Kali): 10.9.0.200/24
- APP-TEST / AUTH-DNS: 172.16.6.20
- DMZ-WEB: 172.16.6.10
3. Nội dung thực hành
TH1 – Chuẩn bị môi trường DNS-LAB
- Tạo snapshot các máy ảo trước khi thay đổi.
- Tạo mạng ảo DNS-LAB riêng, không ảnh hưởng LAN-DOMAIN.
- Thêm interface DNSLAB trên pfSense, đặt IP 10.9.0.1/24.
- Thiết lập firewall rules: cho phép DNS-SERVER đến AUTH-DNS (TCP/UDP 53), truy cập web DMZ (TCP 80), chặn kết nối đến LAN-DOMAIN, MGMT và các lưu lượng còn lại.
TH2 – Cấu hình DNS-SERVER BIND9
- Cấu hình Ubuntu Server với IP 10.9.0.10/24.
- Cài BIND9 và dnsutils.
- Cấu hình zone thuận lab9.test, zone nghịch và forward external.lab9.test đến 172.16.6.20.
- Kiểm tra cấu hình bằng named-checkconf, named-checkzone và dig.
TH3 – Cấu hình Victim và Attacker
- Đặt IP Victim 10.9.0.100/24, sử dụng DNS 10.9.0.10.
- Đặt IP Kali 10.9.0.200/24, cài Scapy, Wireshark và tcpdump.
- Chuẩn bị trang web giả lập trên Kali, chỉ hiển thị nội dung mô phỏng.
- Giới hạn bắt gói trong mạng ảo DNS-LAB.
TH4 – Kiểm tra DNS ban đầu (Baseline)
- Khởi động AUTH-DNS mô phỏng trên APP-TEST 172.16.6.20.
- Kiểm tra www.external.lab9.test phân giải hợp lệ về 172.16.6.10.
- Bắt và quan sát gói DNS bằng Wireshark.
TH5 – Task 1: HOSTS-file Redirection
- Sao lưu và chỉnh sửa file /etc/hosts trên Victim.
- Ánh xạ www.lab9.test đến 10.9.0.200.
- So sánh kết quả getent/curl với dig truy vấn trực tiếp DNS-SERVER.
- Khôi phục file hosts sau thử nghiệm.
TH6 – Task 2: Direct DNS Spoofing
- Xóa DNS cache và tạo truy vấn mới từ Victim.
- Quan sát phản hồi DNS giả trực tiếp đến Victim trong mạng LAB.
- Kiểm tra transaction ID, UDP port và địa chỉ IP trả về bằng Wireshark.
- Đối chiếu IP hợp lệ 172.16.6.10 với IP mô phỏng 10.9.0.200.
TH7 – Task 3: DNS Cache Poisoning
- Xóa cache BIND9 trước khi thử nghiệm.
- Quan sát tình huống phản hồi giả hướng đến DNS Resolver.
- Kiểm tra kết quả phân giải và nội dung cache DNS-SERVER.
- Ghi nhận ảnh hưởng của TTL (120 giây trong mô hình).
TH8 – Khôi phục và phòng thủ
- Dừng các chương trình mô phỏng; khôi phục file hosts và xóa cache DNS.
- Xác nhận DNS trở lại IP hợp lệ 172.16.6.10.
- Đưa Promiscuous Mode về Deny.
- Kiểm thử lại với DNS COOKIE mặc định; ghi nhận sự khác biệt.
- Đề xuất phân đoạn mạng, kiểm soát DNS egress, DNSSEC và giám sát DNS.
TH9 – Xử lý sự cố và câu hỏi phân tích
- Kiểm tra IP, route, firewall rules, BIND9 và Wireshark khi xảy ra lỗi.
- Trả lời 10 câu hỏi phân tích trong tài liệu LAB.
4. Ảnh minh chứng
- LAB8_pfSense_Interface.png: Interface DNSLAB 10.9.0.1/24.
- LAB8_Firewall.png: Firewall rules cô lập DNSLAB.
- LAB8_IP.png: IP DNS-SERVER, Victim và Kali.
- LAB8_BIND9.png: Kiểm tra cấu hình và zone BIND9.
- LAB8_Baseline.png: DNS hợp lệ trả về 172.16.6.10.
- LAB8_Hosts.png: Task 1 – chuyển hướng bằng file hosts.
- LAB8_DNS_Spoofing.png: Task 2 – truy vấn và phản hồi DNS giả trong Wireshark.
- LAB8_Cache_Poisoning.png: Task 3 – phản hồi giả và cache DNS.
- LAB8_Restore.png: DNS trở về 172.16.6.10 sau khôi phục.
- LAB8_Defense.png: Kiểm tra cấu hình phòng thủ và Promiscuous Mode.
Ảnh minh chứng được bổ sung theo kết quả thực hành thực tế; không sử dụng ảnh mẫu làm kết quả.
5. Báo cáo
- Lab8.docx: Báo cáo thực hành, ảnh minh chứng và 10 câu hỏi phân tích.
6. Kênh Youtube
https://www.youtube.com/@HungNguyen-zv9su
