# TIẾN ĐỘ THỰC HÀNH LAB 10 (DNS CACHE POISONING)

## 1. Phân bổ máy ảo (VMware)
* **pfSense**: Gateway `10.9.0.1`, `10.10.0.1`, `172.16.6.1`
* **Client-A** (VICTIM): `10.9.0.100/24` | Mạng: `dns-lab`
* **Client-B** (DNS-SERVER): `10.9.0.10/24` | Mạng: `dns-lab`
* **Ubuntu-18** (ATTACKER): `10.10.0.200/24` | Mạng: `attack-net`
* **DMZ-WEB** (AUTH-DNS + WEB): `172.16.6.10` & `172.16.6.20` | Mạng: `dmz-net`

---

## 2. Phần đã làm xong (✅)
1. **pfSense:** Thêm Adapter 6 `attack-net`, tạo Interface `ATTACKNET` (`10.10.0.1/24`), tạo 3 rules tường lửa cô lập.
2. **Attacker (`Ubuntu-18`):** Nhận IP `10.10.0.200`, Gateway `10.10.0.1`, thông L2 tới pfSense, đã test `tcpdump` xác nhận không sniff được mạng khác.
3. **Victim (`Client-A`):** Nhận IP `10.9.0.100`, Gateway `10.9.0.1`, trỏ DNS về `10.9.0.10`.
4. **DMZ-WEB:** Nhận thêm IP phụ `172.16.6.20`, cài `dnspython`, đang chạy `auth_dns_relay_lab10.py` (port 53, 5300).
5. **Báo cáo:** Đã tạo file `LAB10/LAB10_BaoCao_HoanChinh.docx` (điền sẵn toàn bộ môi trường và 12 câu hỏi lý thuyết).

---

## 3. Việc cần làm tiếp theo (⏳)
1. **Trên `Client-B` (DNS-SERVER):** Chạy Resolver mô phỏng:
   ```bash
   sudo python3 vuln_resolver_lab10.py
   ```
2. **Trên `Ubuntu-18` (Attacker):** Chạy 3 dịch vụ:
   * Terminal 1: `sudo python3 evil_dns_lab10.py`
   * Terminal 2: `sudo python3 -m http.server 80 --directory ~/LAB10/fake_site`
   * Terminal 3: `python3 kaminsky_remote_lab10.py` (Chạy tấn công)
3. **Trên `Client-A` (Victim):** Kiểm tra truy vấn đã bị chuyển hướng sang `10.10.0.200` chưa:
   ```bash
   sudo resolvectl flush-caches && resolvectl query www.example.lab10.test
   curl http://www.example.lab10.test
   ```
4. **Hoàn thiện:** Chụp ảnh kết quả dán vào file `LAB10_BaoCao_HoanChinh.docx` và nộp.

---

## 4. Lệnh kiểm tra nhanh trên Terminal các máy
```bash
ip -br addr show dev ens33 && ip route show default
```
