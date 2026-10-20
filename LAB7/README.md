# LAB 7 – Xây dựng chính sách Web Protection trên pfSense + Web Proxy

## 1. Thông tin sinh viên
- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 7

## 2. Môi trường thực hành
- VMware Workstation
- pfSense CE 2.7.2
- Windows Server 2025
- Ubuntu Server 24.04 LTS
- Squid, E2Guardian, ClamAV, Nginx
- LAN: `10.6.0.0/24` (VMnet2)
- DMZ: `172.16.6.0/24` (VMnet3)
- WEB-PROXY: `10.6.0.30/24`

## 3. Nội dung thực hành

### TH1 – Chuẩn bị môi trường
- Kiểm tra máy ảo, cấu hình mạng và IP trên pfSense.
- Xác định các mạng WAN, LAN, DMZ và MGMT.

### TH2 – Cài đặt WEB-PROXY
- Tạo máy Ubuntu Server 24.04 trên VMware.
- Cấu hình 2 CPU, 2 GB RAM, ổ cứng 20 GB.
- Thiết lập IP tĩnh `10.6.0.30/24`.

### TH3 – Cài đặt dịch vụ Web Proxy
- Cài Squid, E2Guardian và ClamAV.
- Cấu hình Proxy tại cổng 8080 và Squid tại cổng 3128.

### TH4 – Cấu hình Website và DNS
- Tạo website mô phỏng trên DMZ-WEB.
- Cấu hình DNS cho domain `lab7.test`.
- Kiểm tra khả năng phân giải tên miền.

### TH5 – Cấu hình pfSense
- Tạo Firewall Alias và Rules.
- Ép Client-A/B truy cập Web qua Proxy.
- Chặn truy cập HTTP/HTTPS trực tiếp.

### TH6 – Xây dựng chính sách Web
- Hard Block, Warning, Temporary Bypass.
- Whitelist và Schedule 60 phút.
- Quét virus bằng ClamAV.
- Kiểm tra giới hạn file tải xuống 100 MB.

### TH7 – Kiểm thử chính sách
- Kiểm thử 10 kịch bản theo yêu cầu LAB 7.
- Chụp ảnh kết quả truy cập, chặn và cảnh báo website.

### TH8 – Kiểm tra Log
- Firewall Log trên pfSense.
- E2Guardian Access Log.
- Squid Access Log và ClamAV.

### TH9 – HTTPS Inspection (Mở rộng)
- Cấu hình SSL MITM và chứng chỉ CA trong môi trường LAB.
- Kiểm tra khả năng lọc nội dung HTTPS.

## 4. Ảnh minh chứng
- `LAB7_VMware.png`: Cấu hình máy ảo.
- `LAB7_Ubuntu.png`: Cài đặt Ubuntu Server.
- `LAB7_IP.png`: Kiểm tra IP WEB-PROXY.
- `LAB7_Proxy.png`: Cấu hình Squid và E2Guardian.
- `LAB7_Firewall.png`: Firewall Rules pfSense.
- `LAB7_Block.png`: Kết quả chặn website.
- `LAB7_Warning.png`: Trang cảnh báo.
- `LAB7_Antivirus.png`: Kiểm thử ClamAV.
- `LAB7_Log.png`: Nhật ký hệ thống.

*Ảnh minh chứng được bổ sung theo kết quả thực hành thực tế.*

## 5. Báo cáo
- `Lab7.docx`: Báo cáo thực hành và 10 câu hỏi phân tích.

## 6. Kênh Youtube
https://www.youtube.com/@HungNguyen-zv9su
