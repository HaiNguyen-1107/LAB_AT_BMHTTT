LAB 4 – Khảo Sát và Đánh Giá Bề Mặt Mạng bằng Nmap
Họ và tên: Nguyễn Xuân Hải
MSSV: 1150070010
Môn học: An Toàn & Bảo Mật Hệ Thống Thông Tin
Lớp: 11_ĐH_HTTT_AT&BMHTTT

Phiên bản môi trường
Hypervisor: VMware Workstation
Máy quét (Scanner): Ubuntu 18.04 – 192.168.17.129
Máy đích (Target): Metasploitable 2 Linux – 192.168.17.130
Dải mạng: 192.168.17.0/24 (VMware Host-Only)
Nmap: 7.60
Cách dựng môi trường
Tạo 2 máy ảo trong VMware Workstation, đặt card mạng cả hai ở chế độ Host-only.
Khởi động Metasploitable 2, đăng nhập msfadmin/msfadmin, xác nhận IP bằng ifconfig.
Khởi động Ubuntu 18, xác nhận IP bằng ip -br addr, kiểm tra Nmap bằng nmap --version.
Ping kiểm tra thông mạch: ping -c 4 192.168.17.130 → thành công, 0% packet loss.
Các tình huống đã thực hiện
Host Discovery – nmap -sn 192.168.17.0/24 – Phát hiện các máy đang hoạt động trong dải mạng.
TCP Connect Scan – nmap -sT 192.168.17.130 – Quét cổng TCP đầy đủ.
SYN Scan – sudo nmap -sS 192.168.17.130 – Quét half-open, cần quyền root.
FIN / Xmas / NULL Scan – sudo nmap -sF/-sX/-sN 192.168.17.130 – Kỹ thuật quét lách firewall.
ACK Scan – sudo nmap -sA 192.168.17.130 – Kiểm tra firewall có lọc cổng không.
UDP Scan – sudo nmap -sU --top-ports 20 192.168.17.130 – Quét 20 cổng UDP phổ biến nhất.
Service & OS Detection – nmap -sV -O 192.168.17.130 – Nhận diện dịch vụ và hệ điều hành.
Aggressive Scan – nmap -A 192.168.17.130 – Quét tổng hợp toàn diện.
NSE Script – nmap --script smb-os-discovery 192.168.17.130 – Lấy thông tin SMB.
Xuất output – nmap -oN output.txt -oX output.xml 192.168.17.130 – Lưu kết quả ra file.
Kết quả PASS / FAIL
Tất cả 10 tình huống thực hiện đều PASS.
Không có lệnh nào thất bại hoặc cho kết quả sai lệch.
