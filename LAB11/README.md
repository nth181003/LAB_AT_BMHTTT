# LAB 11 – Mã hóa đối xứng hiện đại – DES, TripleDES, AES, RC4, Twofish (Java Swing, Python và SQL Server)

## 1. Thông tin sinh viên

* Họ và tên: Nguyễn Tấn Hưng

* MSSV: 1150080018

* Lớp: CNPM1

* Lab: LAB 11

## 2. Môi trường thực hành

* Hệ điều hành: Windows 11

* Nền tảng Java: OpenJDK 17.0.18

* IDE phát triển: Visual Studio Code (Extension Pack for Java, tương thích cấu trúc form NetBeans)

* Quản lý dự án & thư viện: Apache Maven 3.9 (`mssql-jdbc 12.8.1.jre11`, `bcprov-jdk18on 1.78.1`)

* Hệ quản trị CSDL: Microsoft SQL Server 2025 (17.0) (`MSSQLSERVER`, cổng TCP `14333`)

* Công cụ quản trị CSDL: SQL Server Management Studio (SSMS), SQL Server Configuration Manager

* Môi trường Python: Python 3.14.3, thư viện `cryptography 50.0.2`, Tkinter

* Cấu trúc Project: `LAB2_MaHoaHienDai` (`groupId: vn.edu.lab`, `package: week_02`)

* Lớp khởi chạy chính: `week_02.frm_Menu`

## 3. Nội dung thực hành

### TH1 – Khởi tạo dự án Maven và cấu hình Microsoft SQL Server

* Tổ chức cấu trúc phân tầng tách biệt lớp xử lý thuật toán, tiện ích (`CipherUtil`, `FileTextIO`), tầng truy xuất CSDL (`DbConfig`, `HistoryDao`, `UserDao`) và giao diện Swing.

* Bật giao thức TCP/IP, thiết lập cổng cố định `14333` tại mục `IPAll` và kích hoạt chế độ xác thực hỗn hợp trên SQL Server.

* Thực thi script `01_Tao_CSDL.sql` khởi tạo database `LAB2_MaHoaHienDai` cùng hai bảng `dbo.app_users`, `dbo.crypto_history` và chạy `02_Tao_Tai_Khoan_SQL.sql` cấp quyền tối thiểu cho `lab2_user`.

### TH2 – Cài đặt và kiểm thử mật mã khối DES và TripleDES

* Triển khai `DESCipher` (`DES/CBC/PKCS5Padding`, khóa 8 byte, IV 8 byte ngẫu nhiên) và giao diện `frm_DES`.

* Triển khai `TripleDESCipher` (khóa 24 byte, chế độ CBC, đệm PKCS5) và giao diện `frm_TripleDES`.

* Kiểm thử giải mã khôi phục bản rõ, kiểm tra tính ngẫu nhiên của IV và bắt ngoại lệ khi sai khóa hoặc sai độ dài byte.

### TH3 – Triển khai AES-256-GCM và cơ chế đăng ký/đăng nhập

* Cài đặt `AESCipher` sử dụng chế độ xác thực AES-256-GCM (nonce 12 byte, tag 16 byte), dẫn xuất khóa 32 byte bằng `PBKDF2-HMAC-SHA256` (120.000 vòng lặp).

* Xây dựng luồng Register/Login trên `frm_AES`, lưu salt và hash vào `dbo.app_users`, cấp mã phiên `Ticket` 128 bit sau khi đăng nhập thành công.

* Kiểm thử khả năng phát hiện sửa đổi bản mã thông qua ngoại lệ `AEADBadTagException`.

### TH4 – Cài đặt mật mã dòng RC4 và mật mã khối Twofish

* Cài đặt thuật toán `RC4Cipher` (giai đoạn KSA và PRGA, xuất kết quả dạng HEX) trên giao diện `frm_RC4`, đối chiếu với vector kiểm thử chuẩn.

* Tích hợp thư viện BouncyCastle xây dựng `TwofishCipher` (`TwofishEngine` + CBC + PKCS7, khóa 256 bit từ SHA-256) trên `frm_Twofish`, hỗ trợ lưu và nạp lại tệp kèm IV.

### TH5 – Bài tập nâng cao 01: AES-256 chế độ CTR (Java)

* Cài đặt `AESCTRCipher` (nonce 12 byte kết hợp bộ đếm 4 byte) và giao diện `frm_AES_CTR`.

* Kiểm thử mã hóa/giải mã văn bản dài trên 1.000 ký tự, xác nhận kích thước bản mã bằng đúng độ dài byte UTF-8 của bản rõ.

### TH6 – Bài tập nâng cao 02: AES-256 chế độ CBC (Python)

* Xây dựng ứng dụng độc lập `aes_cbc_gui.py` bằng Python (Tkinter và thư viện `cryptography`) với IV 16 byte ngẫu nhiên và đệm PKCS7.

* Chạy kiểm thử tự động qua tham số dòng lệnh `py aes_cbc_gui.py --self-test` và kiểm tra chức năng lưu/mở tệp dữ liệu.

### TH7 – Lưu trữ và đối chiếu lịch sử giao dịch trên SQL Server

* Tích hợp `HistoryDao.tryInsert` sử dụng `PreparedStatement` để lưu vết thao tác và độ dài dữ liệu vào bảng `dbo.crypto_history`.

* Kiểm tra danh sách bản ghi trên `frm_LichSu` và chạy truy vấn đối chiếu trong SSMS qua script `03_Kiem_Tra_Du_Lieu.sql`.

### TH8 – Đánh giá an toàn thuật toán và chế độ hoạt động

* So sánh mức độ bảo mật giữa các hệ mật cũ (DES, 3DES, RC4) và chuẩn hiện đại (AES-256, Twofish).

* Phân tích ưu thế của cơ chế mã hóa có xác thực `AES-GCM` so với `CBC` và `CTR` trong việc chống chỉnh sửa dữ liệu trái phép.

## 4. Ảnh minh chứng

* `LAB11_Menu.png`: Cửa sổ điều hướng chính `frm_Menu`.

* `LAB11_KetNoiSQL.png`: Kết nối thành công tới Microsoft SQL Server trên `frm_KetNoiSQL`.

* `LAB11_DES.png`: Kết quả mã hóa, giải mã và bắt lỗi khóa/Base64 trên `frm_DES`.

* `LAB11_TripleDES.png`: Kết quả kiểm thử khóa 24 byte và thông báo lỗi độ dài trên `frm_TripleDES`.

* `LAB11_AES_GCM.png`: Luồng Register, Login nhận Ticket và kiểm thử tính toàn vẹn trên `frm_AES`.

* `LAB11_RC4.png`: Kết quả sinh chuỗi HEX khớp vector chuẩn trên `frm_RC4`.

* `LAB11_Twofish.png`: Kết quả mã hóa kèm IV và lưu/mở tệp trên `frm_Twofish`.

* `LAB11_AES_CTR.png`: Kết quả kiểm thử văn bản dài trên `frm_AES_CTR`.

* `LAB11_Python_AES_CBC.png`: Kết quả chạy `--self-test` và giao diện Tkinter `aes_cbc_gui.py`.

* `LAB11_LichSu_SSMS.png`: Bảng lịch sử trên `frm_LichSu` và kết quả truy vấn trong SSMS.

*(Ảnh minh chứng được bổ sung theo kết quả thực hành thực tế.)*

## 5. Báo cáo

* `Bao_cao_LAB11_Nguyen_Tan_Hung.docx`: Báo cáo thực hành Mã hóa đối xứng hiện đại – DES, TripleDES, AES, RC4, Twofish (Java Swing, Python và SQL Server).

## 6. Kênh Youtube

* https://www.youtube.com/@HungNguyen-zv9su
