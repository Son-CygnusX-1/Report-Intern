# Các option của Apt-cacher-ng

* Thư mục lưu trữ dữ liệu tải về và hoạt động 
```
CacheDir: /var/cache/apt-cacher-ng

```
* Thư mục lưu trữ log, có thể set trống để vô hiệu hóa đăng nhập
```
LogDir: /var/log/apt-cacher-ng
```
* Nơi cấu hình bổ sung và tìm kiếm tệp
```
SupportDir: /usr/lib/apt-cacher-ng
```
* Đặt cổng kết nối vs HTTP proxy
```
Port:3142
```
* Địa chỉ hoặc tên máy chủ để lắng nghe. set 0.0.0.0 để chỉ lắng nghe IPv4
```
BindAddress: 0.0.0.0
```
* Đặt proxy HTTP khác sẽ được dùng để tải xuống. Có thể bao gồm tên người dùng và mật khẩu
```
Proxy: https://username:proxypassword@proxy.example.net:3129
```
* Kho lưu trữ ánh xạ 
```
Remap-debrep: file:deb_mirror*.gz /debian ; file:backends_debian # Debian Archives
Remap-uburep: file:ubuntu_mirrors /ubuntu ; file:backends_ubuntu # Ubuntu Archives
Remap-cygwin: file:cygwin_mirrors /cygwin # ; file:backends_cygwin # incomplete, please create this file or specify preferred mirrors here
Remap-sfnet:  file:sfnet_mirrors # ; file:backends_sfnet # incomplete, please create this file or specify preferred mirrors here
Remap-alxrep: file:archlx_mirrors /archlinux # ; file:backend_archlx # Arch Linux
Remap-fedora: file:fedora_mirrors # Fedora Linux
Remap-epel:   file:epel_mirrors # Fedora EPEL
Remap-slrep:  file:sl_mirrors # Scientific Linux
Remap-gentoo: file:gentoo_mirrors.gz /gentoo ; file:backends_gentoo # Gentoo Archives
Remap-centos: file:centos_mirrors /centos
```
* Trang ảo có thể truy cập trong trình duyệt web để xem số liệu thống kê và trạng thái
```
ReportPage: acng-report.html
```
* Tệp socket để truy cập thông qua socket Unix cục bộ thay TCP/IP. 
```
SocketPath:/var/run/apt-cacher-ng/socket
```
* `UnbufferLogs: 0` Nếu đặt là 1, các tệp nhật ký được ghi vào đĩa trên mỗi dòng mới. Mặc định là 0, bộ đệm được xóa sau khi ngắt kế nối máy khách. Về mặt kỹ thuật, đây là bí danh tiện lợi cho tùy chọn gỡ lỗi.
* Cho phép thông tin khách hàng mở rộng trong các mục nhật ký. Khi được đặt thành 0, chỉ có loại hoạt động, thời gian và kích thước chuyển được ghi lại.
```
VerboseLog: 1
```
* Lưu trữ pid của quá trình deamon trong tệp văn bản được chỉ định
```
PidFile: /var/run/apt-cacher-ng/pid
```
* Cấm kết nối đi và làm việc mà không có kết nối internet hoặc phản hồi với lỗi 503 trong trường hợp không thể.
```
Offlinemode: 0
```
* Cấm tải xuống từ các vị trí được chỉ định trực tiếp trong yêu cầu của người dùng, tức là tất cả các tải xuống phải được xử lý bởi các phụ trợ ánh xạ được cấu hình sẵn
```
ForceManaged: 0
```
* Ngay trước khi xem xét một tập tin không được ước tính đã hết hạn (sẽ bị xóa). Nếu gía trị được đặt quá thấp và các tệp chỉ mục cụ thể không khả dụng trong một số ngày thì có nguy cơ loại bỏ các tệp gói vẫn hữu ích. (đặt ngày xóa cache)
```
ExThrehold: 4
```
* Tùy chọn sau đây được phép đánh đổi có thể xảy ra: Hết hạn chạy cho đến khi một dữ liệu nhất định được tải xuống thông qua apt-cacher-ng kể từ lần thực hiện hết hạn cuối cùng.
```
ExStartTradeOff: 500m
```
* Bộ đệm cho dữ liệu độ phân giải DNS, hết hạn bởi thời gian chờ này (tính bằng giây)
```
DnsCacheSeconds: 2000
```
* Có thể dùng apt-cacher-ng như một máy chủ web thông thường với bộ tính năng giới hạn, nghĩa là duyệt thư mục, tải xuống bất kỳ tệp nào, loại nội dung dựa trên /etc/mime.types, nhưng không sắp xếp, thực thi mà chỉ chuyển hướng trang. Để làm được điều này, ánh xạ giữa các thư mục ảo và thư mục thực trên máy chủ phải được xác định bằng chỉ thị LocalDirs. Các thư mục ảo và thực được phân tách bằng dầu cách, nhiều cặp được phân tách bằng dấu chấm phảy. Thư mục thực phải là đường dẫn tuyệt đối. Lưu ý vì tên của các thư mục chính đó chung không gian tên với tên kho lưu trữ.
```
LocalDirs: acng-doc /usr/share/doc/apt-cacher-ng
```
* Tìm thấy các tệp gói không còn được liệt kê trong bất kề tệp chỉ mục nào và loại bỏ chúng sau một thời gian an toàn. Tùy chọn này cho phép giữ nhiều phiên bản của gói trong bộ đệm sau khi hết thời gian an toàn.

## Lab

<https://github.com/thaonguyenvan/meditech-thuctap/blob/master/ThaoNV/ghichep-localrepo/ghichep-apt-cacher-ng.md>

Đã cài và cấu hình xong theo tài liệu trên.

### Trường hợp 1:

Trên Client, tải 1 gói về xem có lưu ở trên server cache không.

* Cài đặt `nmap` từ máy client CentOS

![nmap](images_Linux/cache1.png)

![nmap1](images_Linux/cache2.png)

* Kiểm tra xem trên server có lưu cache lại các gói của Nmap không

![nmap2](images_Linux/cache3.png)

Gói các gói của `nmap` sẽ được lưu trong `/var/cache/apt-cacher-ng/centos/7.6.1810/os/x86_64/Pakages` đã cấu hình `ExThreshold` trong file `acgn.conf`

### Trường hợp 2

Trên Client, xóa gói nmap đã cài đặt. Ngắt kết nối ra in ternet của máy thật để đảm bảo tất cả máy ảo đều không ra được mạng.

![cache](images_Linux/th2.1.png)

Vào máy client, chạy lệnh `yum install nmap` kiểm tra xem. Thấy máy client vẫn có thể cài đặt được gói `nmap` về

![cache2](images_Linux/th2.2.png)

Chi tiết tham khảo
<https://www.unix-ag.uni-kl.de/~bloch/acng/html/index.html>
