LAB 9 – Remote DNS Cache Poisoning (Mô phỏng kỹ thuật Kaminsky)
1. Thông tin sinh viên
- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 9
2. Môi trường thực hành
- VMware Workstation
- pfSense CE 2.7.2
- Ubuntu Server 24.04 LTS
- Kali Linux
- BIND9
- Python (môi trường mô phỏng DNS Relay)
- DNS-SERVER: 10.9.0.10/24
- VICTIM: 10.9.0.100/24
- ATTACKER (Kali): 10.10.0.200/24
- pfSense DNSLAB: 10.9.0.1/24
- pfSense ATTACKNET: 10.10.0.1/24
- AUTH-DNS/RELAY: 172.16.6.20
- DMZ-WEB: 172.16.6.10
3. Nội dung thực hành
TH1 – Chuẩn bị môi trường
- Sao lưu cấu hình và tạo snapshot từ LAB 8.
- Kiểm tra máy ảo, cấu hình mạng và IP trên pfSense.
- Giữ nguyên DNSLAB và DMZ.
TH2 – Xây dựng mạng ATTACKNET
- Tạo LAN Segment attack-net trên VMware.
- Thêm và cấu hình interface ATTACKNET trên pfSense.
- Thiết lập IP 10.10.0.1/24.
- Chuyển Kali sang ATTACKNET với IP 10.10.0.200/24.
TH3 – Cấu hình Firewall
- Tạo Firewall Rules trên pfSense.
- Cho phép các luồng DNS cần thiết giữa VICTIM, DNS-SERVER và AUTH-DNS.
- Cô lập ATTACKNET khỏi các mạng LAN/MGMT.
- Kiểm tra và ghi log các kết nối.
TH4 – Cấu hình DNS-SERVER và AUTH-DNS
- Sao lưu cấu hình BIND9 hiện tại.
- Cấu hình forward zone example.lab10.test.
- Thiết lập AUTH-DNS/RELAY tại 172.16.6.20.
- Kiểm tra cấu hình và trạng thái dịch vụ BIND9.
TH5 – Kiểm tra Baseline và Remote
- Kiểm tra phân giải DNS từ VICTIM.
- Xác nhận tên miền www.example.lab10.test trả về IP hợp lệ 172.16.6.10.
- Kiểm tra Kali không thể nghe trộm truy vấn DNS giữa Resolver và AUTH-DNS.
TH6 – Mô phỏng Remote DNS Cache Poisoning
- Thực hiện mô phỏng kỹ thuật Kaminsky trong mạng lab cô lập.
- Theo dõi log Resolver và AUTH-DNS/RELAY.
- Khảo sát vai trò của TXID, UDP Source Port, DNS Cache và NS/Glue.
- Kiểm tra kết quả phân giải DNS sau mô phỏng.
TH7 – Phân tích và đối chiếu kết quả
- So sánh kết quả DNS trước và sau mô phỏng.
- Kiểm tra bản ghi A và delegation NS/Glue.
- Phân tích khả năng quan sát lưu lượng của Kali.
- Đối chiếu kết quả qua log và truy vấn DNS thực tế.
TH8 – Khôi phục và Hardening
- Khôi phục cấu hình BIND9 ban đầu.
- Giới hạn quyền truy vấn đệ quy bằng ACL.
- Kiểm tra UDP Source Port Randomization và DNSSEC Validation.
- Xóa các Firewall Rules tạm thời.
- Kiểm tra lại DNS sau khi hardening.
4. Ảnh minh chứng
- LAB9_VMware.png: Cấu hình máy ảo trên VMware.
- LAB9_Attacknet.png: Tạo mạng ATTACKNET.
- LAB9_pfSense.png: Cấu hình interface và Firewall Rules.
- LAB9_Kali.png: Cấu hình IP Kali Linux.
- LAB9_BIND9.png: Cấu hình DNS-SERVER và BIND9.
- LAB9_AUTH_DNS.png: Cấu hình AUTH-DNS/RELAY.
- LAB9_Baseline.png: Kết quả kiểm tra DNS ban đầu.
- LAB9_Remote.png: Kiểm tra khả năng cô lập mạng attacker.
- LAB9_Poisoning.png: Kết quả mô phỏng DNS Cache Poisoning.
- LAB9_Log.png: Nhật ký DNS và kết quả kiểm thử.
- LAB9_Hardening.png: Kết quả khôi phục và bảo mật DNS.
Ảnh minh chứng được bổ sung theo kết quả thực hành thực tế.
5. Báo cáo
- Bao_cao_LAB9_Nguyen_Tan_Hung.docx: Báo cáo thực hành Remote DNS Cache Poisoning, mô phỏng kỹ thuật Kaminsky.
6. Kênh Youtube
https://www.youtube.com/@HungNguyen-zv9su
