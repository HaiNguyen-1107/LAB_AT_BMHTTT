# LAB 2 – Mã hóa đối xứng hiện đại

* **Họ và tên:** Nguyễn Xuân Hải
* **MSSV:** 1150070010
* **Lớp:** 11\_ĐH\_TMĐT

## 1. Môi trường triển khai

* **IDE & Ngôn ngữ:** Apache NetBeans IDE, Java (JDK 17+).
* **Project Maven:** `LAB2_MaHoaHienDai` (`package week_02`)
  * Thư viện kết nối CSDL: `com.microsoft.sqlserver:mssql-jdbc` (12.8.1.jre11)
  * Thư viện mật mã: `org.bouncycastle:bcprov-jdk18on` (1.78.1)
* **Hệ quản trị CSDL:** Microsoft SQL Server Express & SSMS
  * Server / Port: `127.0.0.1` / `14333` (TCP/IP Enabled, Mixed Mode Authentication)
  * Database: `LAB2_MaHoaHienDai` (gồm 2 bảng `dbo.app_users` và `dbo.crypto_history`)
  * Tài khoản SQL: `lab2_user` (cấp quyền `db_datareader` và `db_datawriter`)

## 2. Các nội dung đã thực hiện

1. **Khởi tạo Project Maven:** Tạo project `LAB2_MaHoaHienDai`, cấu hình `pom.xml` với chuẩn mã hóa UTF-8, JDK 17 và khai báo các thư viện phụ thuộc (`mssql-jdbc`, `bcprov-jdk18on`).
2. **Xây dựng các lớp tiện ích dùng chung:**
   * `CipherUtil.java`: Chuyển đổi chuỗi ↔ mảng byte (UTF-8), Base64, HEX, sinh số ngẫu nhiên (`SecureRandom`) và dẫn xuất khóa/băm mật khẩu bằng `PBKDF2WithHmacSHA256`.
   * `FileTextIO.java`: Cung cấp hộp thoại mở và lưu tệp văn bản `.txt` (UTF-8) cho các form giao diện.
3. **Thiết lập Cơ sở dữ liệu SQL Server:** Chạy script khởi tạo database `LAB2_MaHoaHienDai`, tạo bảng `dbo.app_users`, `dbo.crypto_history` và tài khoản `lab2_user`.
4. **Xây dựng tầng truy xuất dữ liệu (DAO & Config):**
   * `DbConfig.java`: Lưu cấu hình kết nối trên bộ nhớ và quản lý phiên kết nối JDBC tới SQL Server.
   * `HistoryDao.java`: Ghi và truy vấn lịch sử thao tác vào bảng `dbo.crypto_history` bằng `PreparedStatement`.
   * `UserDao.java`: Xử lý đăng ký, xác thực đăng nhập bằng salt 16-byte + PBKDF2 và cấp phát Ticket 128-bit.
5. **Thiết kế form kết nối SQL Server (`frm_KetNoiSQL.java` - Mục 1.6a):**
   * Thiết kế giao diện nhập thông tin kết nối (`Server`, `Port`, `Database`, `User`, `Password`).
   * Cài đặt sự kiện cho nút **Test Connection** để kiểm tra kết nối tới SQL Server.

## 3. Kết quả đánh giá

* **Biên dịch:** Project biên dịch thành công (`BUILD SUCCESS`), không phát sinh lỗi cú pháp.
* **Tiến độ thực tế:** Đã hoàn thành từ mục 1.1 đến 1.6a; các phần còn lại (mục 1.6b, Phần 2 và Phần 3) chưa thực hiện.

## 4. Danh mục file đính kèm

* `LAB2_MaHoaHienDai/`: Thư mục mã nguồn project Maven trên NetBeans.
* `README.md`: Tài liệu tóm tắt báo cáo thực hành.