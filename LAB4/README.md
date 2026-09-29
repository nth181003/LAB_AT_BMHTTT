# LAB 4 – Khảo sát và đánh giá bề mặt mạng bằng Nmap

## 1. Thông tin sinh viên

- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 4

## 2. Môi trường thực hành

- Hệ điều hành: Windows Server 2025 Datacenter Evaluation
- Kiến trúc: 64-bit
- VMware Workstation
- Command Prompt (CMD)
- Nmap 7.991
- Npcap 1.88
- Mạng Host-Only
- Dải mạng thực hành: 192.168.252.0/24

## 3. Nội dung đã thực hiện

### TH1 – Kiểm tra và thiết lập môi trường Nmap

- Kiểm tra phiên bản Nmap trên máy Scanner.
- Kiểm tra địa chỉ IP Host-Only của máy Scanner.
- Xác định dải mạng Host-Only sử dụng trong bài thực hành.

### TH2 – Host Discovery

- Thực hiện quét Host Discovery bằng tùy chọn `-sn`.
- Quét mạng Host-Only `192.168.252.0/24`.
- Xác định các host đang hoạt động trong mạng.
- Ghi nhận địa chỉ IP và thông tin MAC/vendor do Nmap phát hiện.

### TH3 – Lưu kết quả quét

- Sử dụng tùy chọn `-oN` để lưu kết quả Nmap.
- Lưu kết quả Host Discovery vào file `discovery.txt`.
- Kiểm tra file output sau khi tạo.

## 4. Danh sách bằng chứng

| File | Nội dung |
|---|---|
| Nmap_Version.png | Kiểm tra phiên bản Nmap trên máy Scanner |
| Scanner_IP.png | Kiểm tra địa chỉ IP Host-Only của máy Scanner |
| Host_Discovery.png | Kết quả Host Discovery bằng tùy chọn `-sn` |
| Discovery_Output.png | Lưu kết quả Host Discovery vào file `discovery.txt` |

## 5. File báo cáo

- `LAB4_Nmap.docx`: Báo cáo thực hành LAB 4.

## 6. Kênh Youtube

[https://www.youtube.com/@HungNguyen-zv9su](https://www.youtube.com/@HungNguyen-zv9su)
