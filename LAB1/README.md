Họ tên: Nguyễn Xuân Hải
Lớp: 11_TMĐT
MSSV:1150070010
Lab 1.2 : Bắt gói tin Telnet - SSH 
NỘI DUNG ĐÃ THỰC HIỆN
Thiết lập & Kiểm tra môi trường:
Kiểm tra địa chỉ IP máy chủ Ubuntu Server 18.04 (192.168.18.128) và trạng thái lắng nghe trên cổng 22 (SSH) và 23 (Telnet).
Thực nghiệm Telnet (Port 23):
Đăng nhập với mật khẩu cơ bản (MSSV: 1150070010) và thực thi câu lệnh quản trị.
Kiểm chứng nâng cao: Đổi sang mật khẩu phức tạp (Mk12345678@) và phân tích luồng TCP Stream trên Wireshark.
Thực nghiệm SSH (Port 22):
Kết nối và xác thực qua kênh truyền mã hóa bảo mật.
Bắt gói tin và phân tích cơ chế bảo vệ dữ liệu (Encrypted Payload).
Mở rộng (Demo Public-Key Authentication):
Khởi tạo cặp khóa RSA trên Client Windows 11 bằng PowerShell (ssh-keygen).
Nạp Public Key vào máy chủ và đăng nhập SSH thành công không cần mật khẩu.
Hoàn thành báo cáo:
Trả lời đầy đủ và chi tiết 11 câu hỏi phân tích bảo mật theo yêu cầu.
KẾT QUẢ THỰC HIỆN
Chứng minh dữ liệu truyền qua Telnet hoàn toàn ở dạng văn bản rõ (Plaintext), làm lộ 100% tài khoản, mật khẩu (kể cả mật khẩu phức tạp) và nội dung lệnh.
Chứng minh SSH mã hóa toàn bộ dữ liệu truyền tải trên mạng, bảo đảm 3 thuộc tính an toàn thông tin (Confidentiality, Integrity, Authentication).
Thực nghiệm thành công phương thức đăng nhập bằng SSH Key an toàn.
LƯU Ý:
Môi trường Server: Ubuntu Server 18.04 (IP: 192.168.18.128).
Môi trường Client: Windows 11 (IP: 192.168.18.1), PuTTY 0.85, Wireshark 4.6.8.
Bộ lọc Wireshark:
Telnet: tcp.port == 23
SSH: tcp.port == 22
