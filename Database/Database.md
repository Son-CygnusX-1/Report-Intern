## Phân quyền trong SQL
Đặt mật khẩu root cho MySQL với lần đăng nhập đầu
```
mysqladmin -u root passwork <mật khẩu>
```
Với lần đăng nhập sau khi muốn vào mySQL với quyền root
```
mysql -u root -p
```
Tạo tài khoản MySQL mới
```
CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
```

Sau đó phân quyền cho user

`GRANT [loại quyền] ON [tên database].[tên bảng] TO 'username'@'localhost';`
Có thể sử dụng `*` để đặt tên bảng khi chúng ta muốn truy cập vào tất cả dữ liệu/bảng
Hoặc sử dụng `*.*` để cấp cho người dùng có quyền trên tất cả các cơ sở dữ liệu.
Có một số loại quyền phổ biến:
* **ALL PRIVILEGES** - Cho phép truy cập đầy đủ vào một cơ sở dữ liệu cụ thể. Nếu một cơ sở dữ liệu không được chỉ định, thì cho phép truy cập hoàn toàn vào toàn bộ MySQL.
* **CREATE** - Cho phép người dùng tạo databases và tables
* **DELETE** - Cho phép người dùng xóa rows (hàng) từ một tables
* **DROP** - Cho phép người dùng xóa databases và tables
* **EXECUTE** - Cho phép người dùng thực
* **INSERT**
* **UPDATE**
* **SELECT**

Để thay đổi có hiệu lực và đặc quyền được lưu, lệnh sau phải được thực hiện ở cuối
```
FLUSH PRIVILEGES
```

* Xóa người dùng MySQL
```
DROP USER 'user'@'localhost'
```

## Các loại database
### 1. Hệ thống cơ sở quản lý dữ liệu - RDBMS (Oracle, MySQL, MS server, PostgreSQL)
Relational database management system - RDBMS
Các RDBMS lưu trữ dữ liệu dạng "quan hệ": các bảng với dòng và cột nơi mọi thông tin dữ liệu được lưu trữ như một giá trị của một ô cụ thể. Dữ liệu trong một RDBMS được quản lý thông qua giao thức SQL (ngôn ngữ truy vấn cấu trúc).
**Điểm mạnh** hữu dụng trong việc xử lý các dữ liệu được cấu trúc kỹ càng và hỗ trợ ACIC

*Tính nguyên tố (Atomicity)* một giao dịch có nhiều thao tác khác biệt thì hoặc là toàn bộ các thao tác hoặc là không một thao tác nào được hoàn thành.
*Tính nhất quán (Consistency)* Một giao dịch hoặc là sẽ tạo ra một trạng thái mới và hợp lệ cho dữ liệu, hoặc trong trường hợp có lỗi sẽ chuyển toàn bộ dữ liệu về trạng thái trước khi thực thi giao dịch.
*Tính độc lập (Isolation)* Một giao dịch dạng thực thi và chưa được xác nhận phải bảo đảm tách biệt khỏi các giao dịch khác.
*Tính bền vững (Durability)* Dữ liệu được xác nhận sẽ được hệ thống lưu lại sao cho ngay cả trong trường hợp hỏng hóc hoặc có lỗi hệ thống, dữ liệu vẫn đảm bảo trong trạng thái chuẩn xác.

Dữ liệu được lưu trữ và truy vấn dễ dàng bằng các lệnh truy vấn SQL. Cấu trúc dữ liệu có thể được mở rộng nhanh chóng. Có khả năng cấp quyền truy xuất và chỉnh sửa thông tin cho các loại người dùng khác nhau.

**Điểm yếu**

Không xử lý tốt các dữ liệu phi cấu trúc. Các dữ liệu khi bị chia cắt cần được viết lại dưới dạng khác dễ đọc hơn là ở dạng bảng tính (table), và tốc độ xử lý dữ liệu khá chậm. Việc thay đổi cơ sở dữ liệu dạng RDBMS cũng khá khó vì quy củ chặt chẽ của nó.
RDBMS tốn nhiều chi phí hơn các hệ thống cơ sở dữ liệu khác trong việc xây dựng và phát triển

*Nên dùng trong trường hợp nào?*
- Các trường hợp khi giữ vững tính toàn vẹn dữ liệu - dữ liệu không thể bị chỉnh sửa dễ dàng là tối cần thiết
- Các lĩnh vực tự động hóa
- Thông tin nội bộ

### 2. Document store( MongoDB, Couchbase)
Được gọi là CSDL hướng tài liệu, một thiết kế riêng biệt cho việc lưu trữ tài liệu văn kiện JSON, BSON hoặc XML. Vì cấu trúc dữ liệu không ràng buộc khác với SQL, các CSDL này không đòi hỏi người dùng tự tạo bảng nhập liệu trước khi nhập dữ liệu vào. Các tài liệu có thể chứa bất kì dữ liệu nào. CSDL dạng ày có các cặp khóa - giá trị nhưng cũng có đính kèm các trị số metadata giúp việc query dễ dàng hơn.

**Điểm mạnh**

* Linh hoạt, có thể xử lý dữ liệu nửa cấu trúc và không cấu trúc rất tốt. Người dùng không cần quan tâm tới dạng dữ liệu khi setup, điều này tốt trong trường hợp bạn không lường trước được dạng dữ liệu nào bạn sẽ cần lưu trữ.
* Người dùng có thể thiết kế một cấu trúc cho một tài liệu cụ thể mà không ảnh hưởng tới các tài liệu khác.  Scheme cho CSDL cũng có thể được tùy chỉnh mà không gây ra downtime, giúp high availability. Thời gian ghi dữ liệu cũng rất nhanh.
* Dễ dàng mở rộng theo chiều ngang. Có thể mở rộng nhanh và dễ dàng.

**Điểm yếu**

* CSDL dạng lưu trữ tai liệu hy sinh các yếu tố ACID để đổi lấy sự linh hoạt. Ngoài ra, truy vấn chỉ có thể được thực hiện trong từng tài liêu, không thể truy vấn nhiều tài liệu khác nhau

*Sử dụng khi*
- Dữ liệu phi cấu trúc hoặc không có cấu truc
- Quản lý nội dung
- Phân tích dữ liệu chuyên sâu
- Tạo mẫu nhanh 

### 3. CSDL dạng khóa - giá trị (Redis, Memcached)
Là kiểu lưu trữ đơn giản nhất trong các loại CSDL NoSQL đồng thời nó cũng là kiểu dữ liệu lưu trữ cho tất cả các HQT CSDL NoSQL. Thông thường, các HQT CSDL Key-value lưu trữ dữ liệu dưới dạng key (là một chuỗi duy nhất) liên kết với value có thể ở dạng chuỗi văn bản đơn giản hoặc các tập, danh sách dữ liệu phức tạp hơn. Quá trình tìm kiếm dữ liệu thường được thực hiện thông qua key, điều này dẫn đến sự hạn chế về độ chính xác.

CSDL chìa khóa - giá trị là một dạng CSDL phi quan hệ nơi mà mỗi giá trị được gán cho một key nhất định, còn được biết đến như associative array - mảng liên tưởng. 

Một "key" là một định danh độc nhất được gán cho một giá trị. Keys có thể là bất cứ thứ gì cho phé bởi DBMS. Trong Redis, ley có thể là một hàm nhị phân lên tới 512MB

"Giá trị" có thể được lưu trữ dưới dạng blob (là kiểu dữ liệu của một cột trong bảng RDBMS, có thể lưu ảnh lớn hoặc dữ liệu văn bản như những thuộc tính) và không cần schema định sẵn. Các giá trị này có thể được gán bất cứ loại giá trị nào:
- Số
- Chuỗi giá trị
- Bộ đếm
- JSON, XML, HTML, PHP
- Nhị phân
- Hình ảnh
- Video ngắn
- Danh sách

**Điểm mạnh**
Linh hoạt, xử lý nhiều loại dữ liệu một cách nhanh chóng. Các "key" được dùng để truy xuất thẳng tới các giá trị tìm kiếm, mà không cần thông qua quá trình index, giúp quá trình tìm kiếm diễn ra nhanh chóng. Tính linh động cũng là một điểm mạnh của CSDL dạng này. key-value có thể được chuyển từ hệ thống này sang hệ thống khác mà không cần code lại, có thể dễ dàng mở rộng theo chiều ngang với chi phí thấp.    

**Điểm yếu**
Tính linh hoạt của key-value bị đánh đổi bằng tính chuẩn xác. Rất khó để truy xuất giá trị chính xác từ CSDL dạng này vì dữ liệu được lưu trữ theo blob, nên kết quả trả về hầu như đều theo blob. Gây khó khăn khi báo cáo số liệu hoặc chỉnh sửa một phần của các giá trị. Và không phải object nào cũng có thể được cấu hình thành cặp key-value được.

*Nên dùng khi*
- Khuyến nghị các sản phẩn / thông tin tương tự
- Thông tin và thiết lập người dùng
- Dữ liệu phi cấu trúc review sản phần, bình luận của blog
- Quản lý session trên diện rộng
- Dữ liệu được truy xuất thường xuyên nhưng không thường xuyên cập nhật.

### 4. Mô hình wide - column (Cassandra, HBase)
### 5. CSDL dạng bộ máy tìm kiếm (Elasticsearch)

## Các loại database hiện nay
1. Cơ sở dữ liệu tập trung
2. Cơ sở dữ liệu phân tán
3. Cơ sở dữ liệu cá nhân
4. Cơ sở dữ liệu người dùng
5. Cơ sở dữ liệu thương mại
6. Cơ sở dữ liệu NoSQL
7. Cơ sở dữ liệu điều hành
8. Cơ sở dữ liệu quan hệ
9. Cơ sở dữ liệu đám mây
10. Cơ sở dữ liệu biểu đồ.

## Enable log mysql

```
vi /etc/my.cnf
```
```
[mysqld]
log_error = /var/log/mysql/error.log
```

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
### Backup và Restore MySQL database
Backup
```
/opt/lampp/bin/mysqldump --user=root --password="" bitnami_wordpress > bitnami_wordpress.sql
```
Tạo một cơ sở dữ liệu mới
```
/opt/lampp/bin/mysql --user=root --password="" -e "CREATE DATABASE myblog"
```
Sử dụng máy khách `mysql` để import vào cơ sở dữ liệu mới
```
/ opt / lampp / bin / mysql --user = root --password = "" --database = myblog <bitnami_wordpress.sql
```
## Hệ quản trị cơ sở dữ liệu
* Khái niệm 
DBMS có thể hiểu là hệ thống được thiết kế để quản lý một khối lượng dữ liệu nhất định với một cách tự động và có trật tự. Các hành động quản lý này bao gồm chỉnh sửa, xóa, lưu thông tin và tìm kiếm trong một nhóm dữ liệu nhất định.
* Vai trò
    - Cung cấp môi trường tạo lập cơ sở dữ liệu
    - Cung cấp cách cập nhật và khai thác dữ liệu
    - Cung cấp các công cụ kiểm soát, điều khiển các truy cập vào cơ sở dữ liệu.
Các hệ quản trị cơ sở dữ liệu phổ biến
1. Oracle: 
2. MySQL: Thích hợp cho các ứng dụng có truy vấn CSDL trên internet
3. Microsoft SQL server
4. PostgreSQL: cho phép lưu trữ các lớp dữ liệu không gian một cách hiệu quả
5. MongoDB: Tập tài liệu dùng NoSQL để truy vấn, viết bởi C++
6. SQlite: thích hợp với các ứng dụng mobile
7. Redis: phát triển theo phong cách NoSQL (key-value)