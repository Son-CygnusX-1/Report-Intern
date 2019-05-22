## install NTP
NTP (network time protocol)
Đây là giao thức đồng bộ thời gian giữa các máy chủ với nhau.

```
yum install NTP
```
File cấu hình trong `/etc/ntp.conf`
Lệnh kiểm tra NTP server đã lấy được giờ chuẩn chưa
```
ntpd -p
```
### Lab
* Server

Cho phép các server trong mạng 172.16.0.0/24 kết nối đến NTP server
```
vi /etc/ntp.conf
restrict 172.16.0.0 mask 255.255.255.0 nomodify notrap
server vn.pool.ntp.org iburst
```
Mở port 123 trên firewalld để chạy dịch vụ
```
firewall-cmd --zone=public --add-port=123/tcp
```

* Client 

```
vi /etc/ntp.conf
server <strong> <ip của server></strong> iburst
restrict default ignore
```
Hoặc cài đặt ntpdate `yum install ntpdate` và cấu hình
```
ntpdate <ip của server>
```
Tạo 1 crontab để check thời gian vào mỗi khoảng thời gian
```
crontab -e
*/5 * * * * /usr/sbin/ntpdate <ip server> 2>&1 | tee -a /var/log/ntpdate.log
```