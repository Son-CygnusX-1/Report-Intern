## Đặt vấn đề

Trong bài này chúng ta sẽ tìm hiểu về file Shadow, ý nghĩa của file Shadow.

## File Shadow

Trước hết chúng ta cần hiểu về cơ chế login/logout và hệ thống. 

Trong Linux, file /etc/passwd là file lưu thông tin user của hệ thống, khi bạn tạo một user mới thì linux sẽ thêm vào một bản ghi mới vào file này. Và điều đặc biệt của file này là quyền của nó là -rw-r--r--. 

Nghĩa là thông tin của User có thể được xem bởi bất kỳ User nào trên hệ thống. Tuy nhiên thuộc tính 'r' là cần thiết vì một số ứng dụng và tool của hệ thống cần đọc file này thì mới có thể chạy chính xác được. Đơn giản như muốn thay đổi tài khoản người dùng khác, nếu chúng ta để file Passwd ở quyền dùng root thì hệ thống của người dùng bình thường sẽ không thể đọc được file Passwd để lấy thông tin user name, home directory...

Vì vậy cần lưu trữ password người dùng trong 1 file mà chỉ 'root' mới đọc được.

Giải pháp mà Linux đưa ra là bổ sung 1 file tên là `etc/shadow` để lưu trữ mật khẩu người dùng. Và file này chỉ được truy cập bởi tài khoản root. Và dĩ nhiên mật khẩu trong file shadow được mã hóa bởi hàm băm.

## Mảng băm mật khẩu

Sử dụng lệnh mã hóa trên terminal
```
mkpasswd -m sha-512 <password>
```
Sinh ra được một chuỗi băm ví dụ như:
```
$6$9AgClypCwlpihrj$MCIdy9h0sp4gKJ/u8xYEEMCr18ZuW83RBRUtu5glD1ZS.PUZ1qVViAWAvx8u2vVFYXT.6Zz0BpxOkbp5C2JF50
```
* Với 2 ký tự đầu là đại diện cho loại mã hóa sử dụng là gì. Ở ví dụ trên $6 là sha-512

Các loại khác:
$1 : MD5
$2 : blowfish
$2a : eksblowfish
$5 : sha256

* Ở giữa 2 ký hiệu $ tiếp theo `9AgClypCwlpihrj` đây được gọi là random data hay còn gọi là salt, được sinh ra để kết hợp với mật khẩu người dùng (user password), để tặng độ bảo mật trong mảng băm.
* Ở trường cuối cùng là giá trị băm của salt + user password. Trong ví dụ này là: MCIdy9h0sp4gKJ/u8xYEEMCr18ZuW83RBRUtu5glD1ZS.PUZ1qVViAWAvx8u2vVFYXT.6Zz0BpxOkbp5C2JF50.

Khi đăng nhập vào hệ thống, bạn nhận user/password, hệ thống sẽ dùng giá trị salt của user + password mà bạn nhập vào để tạo một chuỗi mã hóa. Nếu chuỗi mã hóa này trùng với chuỗi mã hóa trong file /etc/shadow thì sẽ login thành công.


