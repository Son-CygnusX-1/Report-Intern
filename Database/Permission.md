Phân quyền trong SQL
`GRANT [loại quyền] ON [tên database].[tên bảng] TO 'username'@'localhost';`

Có một số loại quyền phổ biến:
* **ALL** - Cho phép truy cập đầy đủ vào một cơ sở dữ liệu cụ thể. Nếu một cơ sở dữ liệu không được chỉ định, thì cho phép truy cập hoàn toàn vào toàn bộ MySQL.
* **CREATE** - Cho phép người dùng tạo databases và tables
* **DELETE** - Cho phép người dùng xóa rows (hàng) từ một tables
* **DROP** - Cho phép người dùng xóa databases và tables
* **EXECUTE** - Cho phép người dùng thực
* **INSERT**
* **UPDATE**
* **SELECT**
* 