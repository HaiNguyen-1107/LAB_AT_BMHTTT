# LAB 6 – Xác thực Active Directory và Chính sách truy cập trên pfSense

- **Họ và tên:** Nguyễn Xuân Hải  
- **MSSV:** 1150070010  
- **Môn học:** An toàn & Bảo Mật Hệ Thống Thông Tin  
- **Lớp:** 11_ĐH_TMĐT

---

## 1. Môi trường triển khai
- **Hypervisor:** VMware Workstation 17 Pro
- **Tường lửa pfSense 2.7.2-RELEASE:** 
  - WAN: 192.168.250.128 (NAT / DHCP)
  - LAN: 10.6.0.1/24 (Mạng nội bộ cấp cho Client)
  - MGMT: 192.168.56.254/24 (Host-Only - Quản trị WebGUI cô lập)
  - DMZ: 172.16.6.1/24 (Vùng máy chủ công cộng)
- **Domain Controller (DC01):** Windows Server 2025 Datacenter (IP: 10.6.0.10/24, Domain: `lab6.test`, tích hợp AD DS, DNS và LDAP)
- **Web Server (DMZ-WEB):** Ubuntu 18.04 LTS chạy Nginx với 4 địa chỉ IP mô phỏng:
  - 172.16.6.10: GENERAL_SITE (Trang web chung)
  - 172.16.6.20: JOB_SITE (Trang việc làm)
  - 172.16.6.30: SOCIAL_SITE (Trang mạng xã hội)
  - 172.16.6.40: RESTRICTED_SITE (Trang web cấm)
- **Client (Client-A):** Ubuntu 18.04 LTS (IP: 10.6.0.21/24, Gateway: 10.6.0.1)

---

## 2. Các nội dung và kịch bản đã thực hiện
1. **Chuẩn bị môi trường mạng:** Cấu hình IP tĩnh, Default Gateway và kiểm tra kết nối thông mạng trên Client-A và DMZ-WEB.
2. **Tích hợp Active Directory (LDAP):** Cấu hình Authentication Server `LAB6-AD` trên cổng 389 với Bind User `svc_pfsense_ldap`. Kiểm tra xác thực thành công cả 2 tài khoản `sv_a` và `sv_b`.
3. **Triển khai Captive Portal:** Khởi tạo Zone `LAB6_USERS` trên interface LAN sử dụng backend LDAP. Người dùng `sv_a` đăng nhập thành công và được chuyển hướng tới trang web Nginx.
4. **Khai báo Aliases:** Định nghĩa các nhóm IP (`CLIENT_A`, `CLIENT_B`, `POLICY_CLIENTS`, `GENERAL_SITE`, `JOB_SITE`, `SOCIAL_SITE`, `RESTRICTED_SITE`) và danh mục cổng dịch vụ (`WEB_PORTS`: 80, 443).
5. **Thiết lập Schedules:** 
   - `LUNCH_WINDOW`: 11:30 – 13:00 (Thứ 2 đến Thứ 6)
   - `WORK_HOURS`: 08:00 – 17:00 (Thứ 2 đến Thứ 6)
6. **Cấu hình chính sách Firewall Rules theo các Kịch bản:**
   - **Kịch bản 1:** Chặn Client-A truy cập JOB_SITE (172.16.6.20) bằng luật Reject; cho phép truy cập GENERAL_SITE (172.16.6.10).
   - **Kịch bản 2:** Cấm RESTRICTED_SITE (172.16.6.40) cho toàn bộ nhóm POLICY_CLIENTS (Client-A & B) có bật tính năng ghi nhật ký (Log).
   - **Kịch bản 3:** Cấu hình Client-B chỉ được truy cập SOCIAL_SITE (172.16.6.30) trong giờ nghỉ trưa LUNCH_WINDOW.
   - **Kịch bản 4:** Giới hạn lưu lượng người dùng chỉ cho phép Web (HTTP/HTTPS qua WEB_PORTS) trong giờ hành chính WORK_HOURS.
   - **Kịch bản 5:** Cô lập an toàn vùng mạng DMZ khỏi mạng LAN (Block DMZ net -> LAN net trên tab DMZ) ngăn chặn máy chủ DMZ khởi tạo kết nối vào mạng nội bộ.
7. **Sao lưu cấu hình:** Xuất file cấu hình tường lửa `config.xml` từ menu Diagnostics > Backup & Restore.

---

## 3. Kết quả đánh giá
- **Độ chính xác:** Toàn bộ các luật tường lửa tuân thủ đúng nguyên tắc First-Match và chính sách bảo mật Default Deny.
- **Kiểm thử thực tế:** Kiểm thửu các kịch bản 1,2 còn 3,4,5 chưa kiểm thử được

---

## 4. Danh mục file đính kèm
- `11TMĐT_Lab6_1150070010_NguyenXuanHai.docx`: Báo cáo thực hành hoàn chỉnh (ảnh chụp minh chứng, bảng kết quả và trả lời 12 câu hỏi).
- `config.xml`: File sao lưu toàn bộ cấu hình pfSense đã áp dụng trong bài Lab.
- `README.md`: Tài liệu tóm tắt báo cáo.
