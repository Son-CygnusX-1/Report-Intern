## Tcpdump

Là công cụ được phát triển nhằm mục đích phân tích các gói dữ liệu mạng theo dòng lệnh. Nó cho phép khách hàng chặn và hiển thị các gói tin được truyền đi hoặc được nhận trên một mạng mà máy tính có tham gia.

### Sử dụng tcpdump
#### 1. Cài đặt
* Trên ubuntu
```
apt-get install tcpdump
```
* Trên CentOS
```
yum install tcpdump
```
#### 2. Một vài lệnh cơ bản
* Xem các interface đang hoạt động
```
tcpdump -D
```
* Bắt gói tin trên interface
```
tcpdump -i <interface>
```
Sau khi dừng, sẽ hiện ra một bảng với các thông số:
- Packet capture: số lượng gói tin bắt được và xử lý.
- Packet received by filter: số lượng gói tin được nhận bởi bộ lọc.
- Packet dropped by kernel: số lượng packet đã bị dropped bởi cơ chế bắt gói tin của hệ điều hành.
Định dạng chung của 1 dòng giao thức tcpdump là:
`time-stamp src > dst:  flags  data-seqno  ack  window urgent options`

|Tên trường|Mô tả|
|Time-stamp|hiển thị thời gian gói tin được capture.|
|Src và dst|hiển thị địa IP của người gửi và người nhận.|
|Cờ Flag|S(SYN): Được sử dụng trong quá trình bắt tay của giao thức TCP.
(ACK): Được sử dụng để thông báo cho bên gửi biết là gói tin đã nhận được dữ liệu thành công.
F(FIN): Được sử dụng để đóng kết nối TCP.
P(PUSH): Thường được đặt ở cuối để đánh dấu việc truyền dữ liệu.
R(RST): Được sử dụng khi muốn thiết lập lại đường truyền.|
|Data-sqeno|Số sequence number của gói dữ liệu hiện tại.|
|ACK|Mô tả số sequence number tiếp theo của gói tin do bên gửi truyền (số sequence number mong muốn nhận được).|
|Window|Vùng nhớ đệm có sẵn theo hướng khác trên kết nối này.|
|Urgent|Cho biết có dữ liệu khẩn cấp trong gói tin.|

* Bắt n gói tin với tùy chọn `-c`
Mặc định, `tcpdump` sẽ bắt liên tiếp các gói tin. Để dừng quá trình này.
```
tcpdump -c 10 -i ens33
```
* Lưu file .pcap
```
tcp -i ens33 -w /opt/test.pcap
```
* Đọc file .pcap
```
tcpdump -r test.pcap
```
* Chỉ bắt các gói TCP
```
tcpdump -i ens33 tcp -c 5
```
* Bắt gói theo port
```
tcpdump -i ens33 port 22 -c 5 -n
```
`-n` hiển thị số port thay cho giao thức.
* Bát theo địa chỉ nguồn hoặc đích
```
tcpdump -i ens33 src/dst <ip>
```