# LAB 10 – Mã hóa đối xứng cổ điển và lưu trữ lịch sử trên Microsoft SQL Server

## 1. Thông tin sinh viên
- Họ và tên: Nguyễn Tấn Hưng
- MSSV: 1150080018
- Lớp: CNPM1
- Lab: LAB 10

## 2. Môi trường thực hành
- Hệ điều hành: Windows 11
- Nền tảng Java: OpenJDK 17 (Temurin 17.0.18)
- IDE phát triển: Apache NetBeans (GUI Builder)
- Quản lý dự án & thư viện: Apache Maven (`mssql-jdbc 12.8.1.jre11`)
- Hệ quản trị CSDL: Microsoft SQL Server 2022 Express (`SQLEXPRESS`, cổng TCP `14333`)
- Công cụ quản trị CSDL: SQL Server Management Studio (SSMS)
- Cấu trúc Project: `LAB1_MaHoaCoDien` (`groupId: vn.edu.lab`, `package: week_01`)
- Lớp khởi chạy chính: `week_01.frm_Menu`

## 3. Nội dung thực hành

### TH1 – Khởi tạo dự án và tổ chức cấu trúc chương trình
- Khởi tạo dự án Maven trên Apache NetBeans và khai báo phụ thuộc `mssql-jdbc` trong `pom.xml`.
- Tổ chức phân tách tầng xử lý thuật toán (Java thuần) và tầng giao diện đồ họa (Swing `JFrame`).
- Xây dựng tiện ích đọc/ghi tệp văn bản chuẩn UTF-8 (`FileTextIO`) và cơ chế kiểm tra tính hợp lệ của khóa.

### TH2 – Cài đặt các thuật toán mã hóa thay thế cổ điển
- Cài đặt thuật toán dịch vòng `CaesarCipher` và giao diện `frm_Caesar`.
- Cài đặt thuật toán đa bảng `VigenereCipher` và giao diện `frm_Vigenere`.
- Cài đặt thuật toán ma trận $5 \times 5$ `PlayfairCipher` và giao diện `frm_Playfair`.
- Cài đặt thuật toán khóa tự động `AutokeyCipher` và giao diện `frm_Autokey`.

### TH3 – Cài đặt các thuật toán mã hóa hoán vị
- Cài đặt thuật toán hàng rào `RailFenceCipher` theo quỹ đạo zíc-zắc $k$ hàng và giao diện `frm_RailFence`.
- Cài đặt thuật toán hoán vị cột `TranspositionCipher` theo thứ tự hoán vị $1 \dots m$ và giao diện `frm_Transposition`.

### TH4 – Xây dựng giao diện điều hướng và chương trình tổng hợp
- Thiết kế màn hình chính `frm_Menu` điều hướng toàn bộ các chức năng của ứng dụng.
- Xây dựng lớp điều phối `CipherTongHop` và giao diện `frm_TongHop` sử dụng `JComboBox` chọn thuật toán và nạp khóa mẫu tự động.

### TH5 – Cấu hình Microsoft SQL Server và phân quyền tối thiểu
- Bật giao thức TCP/IP, cố định cổng lắng nghe `14333` và kích hoạt chế độ xác thực hỗn hợp trên SQL Server.
- Chạy script `01_Tao_CSDL.sql` khởi tạo database `LAB1_MaHoaCoDien` và bảng `dbo.history`.
- Chạy script `02_Tao_Login_MAU.sql` tạo tài khoản `lab1_user` với quyền tối thiểu (`SELECT`, `INSERT`, `DELETE`) trên bảng `dbo.history`.

### TH6 – Tích hợp lưu trữ và truy xuất lịch sử giao dịch
- Xây dựng `frm_KetNoiSQL` và `DbConfig` lưu thông tin kết nối tạm thời trên RAM (mật khẩu lưu bằng mảng `char[]`).
- Cài đặt `HistoryDao` sử dụng `PreparedStatement` để ghi nhật ký thao tác và hiển thị dữ liệu lên `JTable` tại `frm_LichSu`.
- Đối chiếu số lượng và nội dung bản ghi trong SSMS bằng truy vấn từ `03_Kiem_Tra_Du_Lieu.sql`.

### TH7 – Thực nghiệm phân tích và tấn công mật mã cổ điển
- Cài đặt lớp `AttackDemos` và giao diện thám mã `frm_TanCong`.
- Thực hiện vét cạn toàn bộ 26 khóa trên bản mã Caesar kết hợp chấm điểm tần suất tiếng Anh.
- Thực hiện phân tích tần suất chữ cái trên bản mã dài và tấn công biết trước bản rõ (Known-Plaintext) để tìm khóa Vigenère.

### TH8 – Kiểm thử tổng thể và đánh giá an toàn hệ mật
- Chạy kiểm thử mã hóa và giải mã trên bộ dữ liệu chuẩn cho cả sáu thuật toán, kiểm tra bắt ngoại lệ khi nhập sai khóa.
- Đánh giá điểm yếu về không gian khóa và đặc trưng thống kê của mật mã cổ điển so với chuẩn hiện đại.

## 4. Ảnh minh chứng
- `LAB10_Menu.png`: Giao diện điều hướng chính `frm_Menu`.
- `LAB10_Caesar.png`: Kết quả kiểm thử mã hóa và giải mã trên `frm_Caesar`.
- `LAB10_Vigenere.png`: Kết quả kiểm thử mã hóa và giải mã trên `frm_Vigenere`.
- `LAB10_RailFence.png`: Kết quả kiểm thử trên `frm_RailFence`.
- `LAB10_Playfair.png`: Kết quả mã hóa kèm ma trận khóa $5 \times 5$ trên `frm_Playfair`.
- `LAB10_Transposition.png`: Kết quả kiểm thử hoán vị cột trên `frm_Transposition`.
- `LAB10_Autokey.png`: Kết quả kiểm thử khóa tự động trên `frm_Autokey`.
- `LAB10_TongHop_LichSu.png`: Giao diện `frm_TongHop` và bảng lịch sử `frm_LichSu`.
- `LAB10_SSMS.png`: Kết quả truy vấn kiểm chứng dữ liệu bảng `dbo.history` trong SSMS.
- `LAB10_TanCong.png`: Kết quả thực nghiệm vét cạn Caesar, phân tích tần suất và Known-Plaintext trên `frm_TanCong`.

*(Ảnh minh chứng được bổ sung theo kết quả thực hành thực tế.)*

## 5. Báo cáo
- `Bao_cao_LAB10_Nguyen_Tan_Hung.docx`: Báo cáo thực hành Mã hóa đối xứng cổ điển và lưu trữ lịch sử trên Microsoft SQL Server.

## 6. Kênh Youtube
- https://www.youtube.com/@HungNguyen-zv9su
