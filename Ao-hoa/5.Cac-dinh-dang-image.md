## 1. File image trong KVM

* File image của đĩa CD/DVD chính là một dạng file có định dạng theo các chuẩn tạo file ảnh. File image là một file đóng gói hết tất cả nội dung của một đĩa CD/DVD vào trong nó.
* Trong KVM Guest có 2 thành phần chính đó là VM dèinition lưu dưới dạng file xml tại `etc/libvirt/qemu` File này chứa các thông tin của máy ảo như tên, số ram, số CPU... File còn lại là srorage thường được lưu dưới dạng file image tại thư mục `/var/lib/libvirt/images`
* 3 định dạng thông dụng nhất của file image sử dụng trong KVM là ISO, raw và qcow2

## 2. Định dạng file image phổ biến trong KVM

### 2.1 File ISO

* File ISO là file ảnh của 1 đĩa CD/DVD, nó chứa toàn bộ dữ liệu của đĩa CD/DVD đó.
* Boot file từ ISO cũng là một trong số những tùy chọn mà người dùng có thể sử dụng khi tạo máy ảo.

### 2.2 File raw

* Là định dạng file image phi cấu trúc
* Định dạng raw là định dạng theo dạng nhị phân của ổ đĩa
* KHi tạo mới một máy ảo có disk format là raw thì dung lượng của file disk sẽ đúng bằng dung lượng của ổ đĩa ảobạn đã tạo ra.
* Mặc định khi tạo với virt-manager hoặc không khai báo với virt-install thì định dạng sẽ là raw. (raw là định dạng mặc định của QEMU)

### 2.3 File qcow2

* qcow là một định dạng tập tin cho đĩa hình ảnh các tập tin được sử dụng bởi QEMU, một tổ chức màn hình máy ảo. Nó viết tắt của "QEMU Copy On Write" và sử dụng một chiến lược tố ưu hóa lưu trữ đĩa để trì hoãn phân bổdung lượng lưu trữ cho đến khi nó thực sự cần thiết. Các tập tin trong định dạng qcow có thể chứa một loạt các hình ảnh đĩa thường được gắn liền với khác cụ thể là các hệ điều hành. Hai phiên bản của các định dạng tồn tại: qcow, và qcow2.
* Qcow2 là một phiên bản cập nhật của định dạng qcow, nhằm để thay thế nó. Khác biệt với bản gốc là Qcow2 hỗ trợ nhiều snapshot thông qua một mô hình mới, linh hoạt để lưu trữ ảnh chụp nhanh. Khi khởi tạo máy ảnh mới sẽ dựa vào disk này rồi snapshot thành một máy mới.
* Qcow2 hỗ trợ copy-on-write với những tính năng đặc biệt như snapshot, mã hóa, nén dữ liệu...
    * Các tập tin dạng này có thể phát triển khi dữ liệu được thêm vào.
    * Cho phép lưu trữ các thay đổi được thực hiện với một hình ảnh cơ sở chỉ đọc trên một tập tin qcow riêng biệt bằng cách sử dụng copy on write.
    * Tính năng tùy chọn bao gồm AES mã hóa và zlib dựa trên giải nén trong suốt
    * Không thể gán trực tiếp như với raw disk.
* Copy on write(cow), đôi khi được gọi là chia sẻ tiềm ẩn, là một kỹ thuật quản lý tài nguyên được sử dụng trong lập trình máy tính để thực hiện có hiệu quả thao tác "nhân bản" hoặc "sao chép" trên các tài nguyên có thể thay đổi.
* Qcow2 hỗ trợ tăng bộ nhớ bằng Thin Provisioning.