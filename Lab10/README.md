# BÁO CÁO THỰC HÀNH LAB 10: REMOTE DNS CACHE POISONING TRONG MÔI TRƯỜNG pfSense CÔ LẬP
TRONG MÔI TRƯỜNG pfSense CÔ LẬP
**Môn học:** An toàn và Bảo mật Hệ thống Thông tin  
**Sinh viên:** Nguyễn Xuân Hải  
**Lớp:** 11_TMĐT  
**MSSV:** 1150070010  

## 1. Phân bổ máy ảo (VMware)
* **pfSense**: Gateway `10.9.0.1`, `10.10.0.1`, `172.16.6.1`
* **Client-A** (VICTIM): `10.9.0.100/24` | Mạng: `dns-lab`
* **Client-B** (DNS-SERVER): `10.9.0.10/24` | Mạng: `dns-lab`
* **Ubuntu-18** (ATTACKER): `10.10.0.200/24` | Mạng: `attack-net`
* **DMZ-WEB** (AUTH-DNS + WEB): `172.16.6.10` & `172.16.6.20` | Mạng: `dmz-net`

---

## 2. Phần đã làm 
1. **Cấu hình các máy ảo** 

