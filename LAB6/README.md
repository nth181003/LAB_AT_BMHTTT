# LAB 6 – Xác thực Active Directory và chính sách truy cập trên pfSense

## 1. Thông tin sinh viên

- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 6

## 2. Môi trường thực hành

- Hệ điều hành máy chủ: Windows Server 2025 Datacenter Evaluation
- Kiến trúc: 64-bit
- VMware Workstation
- pfSense CE 2.7.2-RELEASE
- Command Prompt (CMD)
- Mạng WAN: Bridged
- Mạng LAN: VMware VMnet2
- Mạng DMZ: VMware VMnet3
- Mạng quản trị MGMT: Chưa cấu hình
- Domain dự kiến: `lab6.test`
- LAN theo mô hình đề bài: `10.6.0.0/24`
- DMZ theo mô hình đề bài: `172.16.6.0/24`
- MGMT theo mô hình đề bài: `192.168.56.0/24`

**Lưu ý:** Đề LAB6 yêu cầu 4 interface WAN, MGMT, LAN và DMZ. Cấu hình hiện tại có 3 card mạng nên cần bổ sung card MGMT và kiểm tra lại địa chỉ IP theo mô hình của đề.

## 3. Nội dung thực hiện

### TH1 – Chuẩn bị và cấu hình máy ảo pfSense

- Sử dụng VMware Workstation để quản lý máy ảo pfSense.
- Kiểm tra cấu hình tài nguyên máy ảo.
- Kiểm tra các Network Adapter.
- Cấu hình mạng WAN sử dụng Bridged.
- Cấu hình mạng LAN sử dụng VMware VMnet2.
- Cấu hình mạng DMZ sử dụng VMware VMnet3.
- Bổ sung mạng MGMT theo yêu cầu của LAB6.

### TH2 – Gán các Interface trên pfSense

- Truy cập console pfSense.
- Thực hiện Assign Interfaces.
- Gán các interface theo mô hình LAB6:
  - WAN: Kết nối mạng bên ngoài.
  - MGMT: Mạng quản trị pfSense.
  - LAN: Mạng nội bộ chứa Domain Controller và máy trạm.
  - DMZ: Mạng dành cho máy chủ Web thử nghiệm.
- Xác nhận cấu hình và kiểm tra trạng thái interface.

### TH3 – Cấu hình địa chỉ IP cho các mạng

- WAN: Nhận IP theo cấu hình mạng Bridged hoặc mạng WAN được đề bài quy định.
- MGMT: `192.168.56.254/24`.
- LAN: `10.6.0.1/24`.
- DMZ: `172.16.6.1/24`.
- Kiểm tra địa chỉ IP và khả năng kết nối giữa các máy trong mô hình.

### TH4 – Cấu hình Active Directory và DNS

- Chuẩn bị Windows Server 2025.
- Cấu hình địa chỉ IP tĩnh cho Domain Controller.
- Cài đặt và cấu hình Active Directory Domain Services (AD DS).
- Thiết lập domain `lab6.test`.
- Cấu hình DNS cho domain.
- Tạo OU `LAB6-Users` và các tài khoản thử nghiệm theo yêu cầu bài lab.
- Kiểm tra kết nối từ pfSense đến Domain Controller.

### TH5 – Tích hợp LDAP Authentication Server

- Truy cập **System → User Manager → Authentication Servers** trên pfSense.
- Tạo LDAP Authentication Server với tên `LAB6-AD`.
- Cấu hình địa chỉ máy chủ LDAP và thông tin domain.
- Kiểm tra xác thực tài khoản `sv_a` và `sv_b` tại **Diagnostics → Authentication**.
- Ghi nhận kết quả xác thực thành công hoặc thất bại.

### TH6 – Cấu hình Captive Portal

- Tạo Captive Portal Zone trên pfSense.
- Cấu hình phương thức xác thực LDAP.
- Thực hiện kiểm thử đăng nhập bằng tài khoản domain.
- Chụp ảnh màn hình trang đăng nhập và kết quả xác thực.

### TH7 – Tạo Firewall Alias và Schedule

- Tạo các Alias đại diện cho máy trạm và nhóm website thử nghiệm.
- Cấu hình Schedule theo thời gian được yêu cầu.
- Áp dụng Alias và Schedule vào Firewall Rules.
- Kiểm tra tác động của các chính sách truy cập.

### TH8 – Kiểm thử các chính sách truy cập

- Kịch bản 1: Chặn Client-A truy cập `JOB_SITE`.
- Kịch bản 2: Chặn `RESTRICTED_SITE` đối với Client-A và Client-B.
- Kịch bản 3: Chỉ cho Client-B truy cập `SOCIAL_SITE` trong giờ nghỉ.
- Kịch bản 4: Giới hạn HTTP/HTTPS theo giờ hành chính.
- Kịch bản 5: Cô lập DMZ khỏi LAN nhưng vẫn cho phép các kết nối cần thiết.
- Kiểm tra thứ tự Firewall Rules và ghi nhận kết quả thực tế.

### TH9 – Kiểm tra nhật ký và trạng thái kết nối

- Kiểm tra Firewall Log.
- Kiểm tra State Table.
- Đối chiếu kết quả thực tế với các Firewall Rules đã cấu hình.
- Chụp ảnh minh chứng cho từng kịch bản.

### TH10 – Sao lưu cấu hình

- Truy cập **Diagnostics → Backup & Restore**.
- Tải file cấu hình pfSense `config.xml`.
- Kiểm tra file sao lưu trước khi nộp bài.

## 4. Danh sách bằng chứng

| **File** | **Nội dung** |
|---|---|
| `LAB6_Network.png` | Cấu hình các Network Adapter của pfSense |
| `LAB6_Assign_Interface.png` | Gán WAN, MGMT, LAN và DMZ |
| `LAB6_Interface_IP.png` | Cấu hình địa chỉ IP các interface |
| `LAB6_AD_DNS.png` | Cấu hình Active Directory và DNS |
| `LAB6_LDAP_Test.png` | Kiểm tra xác thực LDAP của `sv_a` và `sv_b` |
| `LAB6_Captive_Portal.png` | Kiểm thử đăng nhập Captive Portal |
| `LAB6_Alias_Schedule.png` | Cấu hình Firewall Alias và Schedule |
| `LAB6_Firewall_Rules.png` | Các quy tắc kiểm soát truy cập |
| `LAB6_Policy_Test.png` | Kết quả kiểm thử các kịch bản |
| `LAB6_Firewall_Log.png` | Nhật ký Firewall |
| `LAB6_State_Table.png` | Bảng trạng thái kết nối |
| `LAB6_Backup.png` | Minh chứng sao lưu cấu hình pfSense |

*Lưu ý: Tên file trên là tên đề xuất. Chỉ ghi nhận những ảnh minh chứng đã thực sự chụp và lưu.*

## 5. File báo cáo

- `Lab6.docx`: Báo cáo thực hành LAB 6.


## 6. Kênh Youtube

[https://www.youtube.com/@HungNguyen-zv9su](https://www.youtube.com/@HungNguyen-zv9su)
