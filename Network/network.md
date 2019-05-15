## Netstat
```
yum install nettools
```
Các command
* Liệt kê tất cả các cổng kết nối TCP và UDP
```
netstat -a | more
```
* Liệt kê tất cả các cổng kết nối TCP
```
netsat -at
```
* Liệt kê tất cả các cổng kết nối UDP
```
netstat -au
```
* Liệt kê các cổng TCP đang lắng nghe
```
netstat -lt
```
* Liệt kê các cổng UDP đang lắng nghe
```
netstat -lu
```
* Liệt kê các cổng Unix dang lắng nghe 
```
netstat -lx
```
* Hiển thị thống kê qua từng giao thức
```
netstat -s
```
* Hiển thị tên dịch vụ với PID
```
netstat -tp
```
* Hiển thị bảng định tuyến
```
netstat -r
```
* Hiển thị trao đổi trên cổng mạng
```
netstat -i
```
* Hiển thị thông tin cổng mạng
```
netstat -ie
```
* Hiển thị một chương trình nào đó đang chạy
```
netstat -ap | grep http
```
* Kiểm tra các dịch vụ nào đang chạy trên port nào
```
netstat -tulpn | grep <name service>
```
## ss
Hiển thị các cổng lắng nghe (sử dụng `-t` để thêm option TCP hoặc `-u` UDP, `-x` UNIX)
```
ss -l
```

* Lọc theo các trạng thái của TCP
- established
- syn-sent
- syn-recv
- fin-wait-1
- fin-wait-2
- time-wait
- closed
- close-wait
- last-ack
- listening
- closing
- all
- connected
- synchronized
- bucket
- syn-recv
- big

ví dụ
```
ss -4 state listening
```
`-4` IPv4
`-6` IPv6
* Hiển thị socket kết nối từ 1 địa chỉ
```
ss dst 192.168.0.1
```