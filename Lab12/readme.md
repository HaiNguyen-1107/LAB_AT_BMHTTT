# LAB 3 - MÃ HÓA KHÓA CÔNG KHAI

* **Họ và tên:** Nguyễn Xuân Hải
* **MSSV:** 1150070010
* **Lớp:** 11\_ĐH\_TMĐT

- **Project:** `LAB3_MaHoaKhoaCongKhai` (Java Maven - package `week_03`)
- **Môi trường:** Apache NetBeans, JDK 17+, Microsoft SQL Server (`mssql-jdbc`)

## 1. Các phần đã hoàn thành
- **Cấu trúc project & lớp dùng chung:**
  - Cấu hình `pom.xml` với thư viện `mssql-jdbc`.
  - `CryptoSupport.java`, `FileTextIO.java`.
- **Cơ sở dữ liệu & kết nối SQL Server:**
  - Tạo CSDL `LAB3_MaHoaKhoaCongKhai`, bảng `dbo.History` và tài khoản `lab3_user`.
  - `DbConfig.java`, `HistoryDao.java`.
  - Form `frm_KetNoiSQL.java` (kết nối & kiểm tra kết nối SQL Server).
  - Form `frm_LichSu.java` (xem lịch sử thao tác từ bảng `dbo.History`).
- **Bài 3.1 - RSA (Console):**
  - `RSACipher.java`, `RSADemo.java` (tạo khóa 2048/3072 bit, mã hóa/giải mã OAEP-SHA256).
- **Bài 3.2 - RSA (Swing):**
  - Form `frm_RSA.java` (tạo khóa, mã hóa/giải mã RSA-OAEP và ghi lịch sử vào SQL Server).

## 2. Các phần chưa hoàn thành
- **Bài 3.3 - ECC:** Chưa làm (`ECCCipher.java`, `frm_ECC.java`).
- **Bài 3.4 - Hệ mã lai RSA + AES:** Chưa làm (`RSA_AES_Cipher.java`, `frm_RSA_AES.java`).
- **Bài 3.5 - Chữ ký số ECDSA:** Chưa làm (`ECCSignature.java`, `frm_ECC_Signature.java`).
- **Phần 3 - Menu chính:** Chưa làm (`frm_Menu.java`).

