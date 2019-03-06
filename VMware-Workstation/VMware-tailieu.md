# VMware Workstation Pro 15

## Giới thiệu

**VMware Workstation Pro:** Là phần mềm giúp bạn tạo máy ảo giả lập nhiều hệ điều hành khác nhau một cách dễ dàng, đây được coi như một trong những phần mềm ảo hoá nổi tiếng mạnh nhất trên thế giới hiện nay. Nó được sử dụng rộng rãi cho các doanh nghiệp, công ty, và chiếm số đông người dùng là cá nhân. Mới đây nhân dịp kỷ nhiệm 20 năm thành lập của hãng đội ngủ VMware vừa cho ra mắt phiên bản VMware Workstation 15 Pro mới nhất trong tháng 9/2018.

**VMware Workstation 15 Pro** được cập nhật và có sự thay đổi rất nhiều về hiệu suất đặc biệt là giao diện có sự đột phá mới mẻ với tông màu xanh lá cây chủ đạo. Đây là bản phát hành lớn nhất mà bạn không thể nào bỏ qua. Với VMware bạn có thể tạo riêng một máy ảo ngay trên máy PC nhầm phục vụ cho việc học, kiểm tra virus, các phần mềm độc hại mà không cần phải lo lắng về mức độ an toàn trên máy thật v.v...

## Các chức năng trong VMware Workstation 15 Pro

### Các mode network trong VMware

* **Bridged**

Sao chép một nút mạng khác trên mạng vật lý và máy ảo sẽ nhận được IP của nó (Nếu DHCP được kich hoạt trong mạng

* **NAT**

Sử dụng ip do máy thật cấp.

* **Hostonly**

Chỉ cho phép hoạt động mạng với hệ điều hành của máy thật.

### Cách thêm và xóa một Network

* Trong VMWare, chọn Edit -> Virtual Network Editor

![Network1](Images-VMWare/Network1.png)

* Nhấn vào Add Network để thêm một card mạng ảo mới hoặc Remove Network để xóa một card mạng đi. Mặc định sẽ có 3 card là *vmnet0(bridged)*, *vmnet1(hostonly)*, *vmnet8(Nat)*

![Network2](Images-VMWare/Network2.png)

### Cấu hình DHCP trong VMware

* Trên hệ điều hành ubuntu, VMware pro 15 không có phần DHCP settings trên giao diện Virtual Network Editor. Nên để vào DHCP setting ta vào bằng lệnh trên Cmd theo đường dẫn /etc/vmware/vmnet10/dhcpd/dhcpd.conf

![DHCP1](Images-VMWare/DHCP1.png)

Ở đây xuất hiện các tham số
*subnet* dải địa chỉ IPnet của mạng 
*netmask* Để tìm số bit net của mạng
*range* Dải IP muốn đặt để cấp cho máy ảo
*option broadcast-address* 
*option domain-name-servers* địa chỉ để đẩy thông tin DNS

Khi đã sửa IP subnet và range DHCP chúng ta khởi động máy ảo(tôi dùng Centos7) và đăng nhập vào hệ thống.

![cenos7](Images-VMWare/cenos7.png)

Lúc này để muốn ra được mạng internet, chúng ta phải up card mạng trong hệ điều hành lên
**ifup ens33**

sau đó kiểm tra ip **ip a** và ping thử đến 8.8.8.8

![cenos7.2](Images-VMWare/cenos7.2.png)

