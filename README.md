# LAB 3 – Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin

## 1. Thông tin sinh viên

- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 3

## 2. Môi trường thực hành

- Hệ điều hành: Windows Server 2025 Datacenter Evaluation
- Kiến trúc: 64-bit
- VMware Workstation
- PowerShell
- Windows Defender Antivirus
- Windows Event Log / Audit Policy

## 3. Nội dung đã thực hiện

### TH1 – Nhận diện và đánh giá rủi ro

- Xây dựng Risk Register.
- Phân loại các nguồn đe dọa:
  - Accidental Action
  - Intentional Action
  - Natural Disaster
  - Technical Error
  - Management Error
- Kiểm tra trạng thái Windows Firewall.

### TH2 – Malware / EICAR

- Kiểm tra trạng thái Windows Defender.
- Kiểm thử mẫu EICAR.
- Quan sát phản ứng của Windows Defender.
- Kiểm tra Protection History.
- Ghi nhận trạng thái quarantine.

### TH3 – Password Attack / Windows Event Log

- Bật Audit Logon.
- Tạo tài khoản lab `lab3user`.
- Thực hiện đăng nhập sai để tạo Event ID 4625.
- Thực hiện đăng nhập thành công để kiểm tra Event ID 4624.
- Thu thập log phục vụ phân tích.

## 4. Danh sách bằng chứng

| File | Nội dung |
|---|---|
| H3_Baseline_Firewall.png | Kiểm tra Windows Firewall |
| H4_ProtectionHistory_EICAR.png | Windows Defender phát hiện và quarantine EICAR |
| H4_Defender_EICAR_Log.png | Log phát hiện EICAR |
| H5_Event4625.png | Đăng nhập thất bại – Event 4625 |
| H5_Event4624.png | Đăng nhập thành công – Event 4624 |
