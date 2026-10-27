# BÁO CÁO THỰC HÀNH LAB 8: LOCAL DNS ATTACK
**Môn học:** An toàn và Bảo mật Hệ thống Thông tin  
**Sinh viên:** Nguyễn Xuân Hải  
**Lớp:** 11_TMĐT  
**MSSV:** 1150070010  


## 1. Mô hình mạng và Phân bổ IP
- **pfSense Router/Firewall**: Interface `DNSLAB` (10.9.0.1/24) trên cổng `em4`, kết nối mạng ảo `dns-lab`.
- **DNS-SERVER (Client-B)**: `10.9.0.10/24` (Gateway: `10.9.0.1`).
- **VICTIM (Client-A)**: `10.9.0.100/24` (Gateway: `10.9.0.1`).
- **ATTACKER (Ubuntu-18)**: `10.9.0.200/24` (Gateway: `10.9.0.1`).


## 2. Thiết lập Tường lửa Cô lập trên pfSense
Thiết lập 5 Rules nghiêm ngặt tại tab `Firewall > Rules > DNSLAB`:
1. **Pass**: `10.9.0.10` -> `172.16.6.20` (UDP/TCP 53) - Truy vấn DNS sang DMZ.
2. **Pass**: `DNSLAB subnets` -> `172.16.6.10` (TCP 80) - Truy cập Web DMZ hợp lệ.
3. **Block + Log**: `DNSLAB subnets` -> `LAN subnets` - Bảo vệ mạng LAN cũ.
4. **Block + Log**: `DNSLAB subnets` -> `MGMT subnets` - Bảo vệ mạng quản trị Host.
5. **Block + Log**: `DNSLAB subnets` -> `Any` - Cô lập tuyệt đối, cấm ra Internet/WAN.


## 3. Nội dung thực hiện: Task 1 - Local Redirection bằng file /etc/hosts
- **Phía Attacker (10.9.0.200)**: Khởi chạy HTTP Server giả lập trên cổng 80:
  ```bash
  mkdir -p ~/fake && cd ~/fake
  echo "<h1 style='color:red'>LAB 9 - TRANG MO PHONG BI CHUYEN HUONG (ATTACKER 10.9.0.200)</h1>" > index.html
  sudo python3 -m http.server 80
  ```
- **Phía Victim (10.9.0.100)**: Chỉnh sửa file `/etc/hosts` chuyển hướng tên miền `www.lab9.test`:
  ```bash
  sudo cp /etc/hosts /etc/hosts.bak
  echo "10.9.0.200  www.lab9.test" | sudo tee -a /etc/hosts
  

## 4. Tệp tin đính kèm
- File báo cáo chi tiết kèm hình ảnh minh chứng: `11TMĐT_Lab8_1150070010_NguyenXuanHai.docx`.
