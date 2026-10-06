# LAB 5 – Thiết lập mô hình tường lửa pfSense

## 1. Thông tin sinh viên

- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 5

## 2. Môi trường thực hành

- Hệ điều hành máy chủ: Windows Server 2025 Datacenter Evaluation
- Kiến trúc: 64-bit
- VMware Workstation
- pfSense CE 2.7.2-RELEASE
- Command Prompt (CMD)
- Mạng WAN: Bridged
- Mạng LAN: VMware VMnet2
- Mạng DMZ: VMware VMnet3
- LAN: 10.0.0.0/8
- DMZ: 172.16.0.0/16

## 3. Nội dung đã thực hiện

### TH1 – Chuẩn bị và cài đặt pfSense

- Tạo máy ảo pfSense trên VMware Workstation.
- Cấu hình tài nguyên cho máy ảo pfSense.
- Cấu hình 3 card mạng cho pfSense:
  - WAN → Bridged
  - LAN → VMnet2
  - DMZ → VMnet3
- Gắn ISO pfSense CE 2.7.2-RELEASE.
- Cài đặt pfSense lên ổ đĩa ảo.
- Khởi động lại pfSense sau khi hoàn tất cài đặt.

### TH2 – Gán các Interface trên pfSense

- Thực hiện Assign Interfaces trên console pfSense.
- Gán interface WAN:
  - `em0 → WAN`
- Gán interface LAN:
  - `em1 → LAN`
- Gán interface DMZ:
  - `em2 → OPT1`
- Xác nhận cấu hình interface trên pfSense.

### TH3 – Cấu hình địa chỉ IP cho mạng LAN

- Truy cập chức năng Set interface(s) IP address trên console pfSense.
- Cấu hình địa chỉ IP cho LAN:
  - IP: `10.0.0.1`
  - Subnet prefix: `/8`
  - Subnet mask: `255.0.0.0`
- Không bật DHCP Server trên LAN.

### TH4 – Cấu hình địa chỉ IP cho mạng DMZ

- Cấu hình interface OPT1 làm vùng DMZ.
- Đặt địa chỉ IP:
  - IP: `172.16.0.1`
  - Subnet prefix: `/16`
  - Subnet mask: `255.255.0.0`
- Không bật DHCP Server trên DMZ.

## 4. Danh sách bằng chứng

| **File** | **Nội dung** |
| -------- | ------------ |
| pfSense_Network.png | Cấu hình 3 card mạng của máy ảo pfSense |
| pfSense_Assign_Interface.png | Gán WAN, LAN và OPT1 trên pfSense |
| pfSense_LAN_IP.png | Cấu hình LAN `10.0.0.1/8` |
| pfSense_DMZ_IP.png | Cấu hình OPT1/DMZ `172.16.0.1/16` |

## 5. File báo cáo

- `LAB5_pfSense.docx`: Báo cáo thực hành LAB 5.

## 6. Kênh Youtube

[https://www.youtube.com/@HungNguyen-zv9su](https://www.youtube.com/@HungNguyen-zv9su)
