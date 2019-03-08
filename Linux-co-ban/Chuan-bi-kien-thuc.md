# Linux

1. [Lịch sử phát triển](#LichSu)
2. [Khái niệm Distro và các distro nổi bật](#Distro)
3. [Phân biệt Linux và Unix](#Linux)
4. [Tìm hiểu các phiên bản của CentOS và Ubuntu](#Version)
5. [Tìm hiểu Kernel, quá trình khởi động của HĐH](#Kernel)
6. [Tìm hiểu các phân vùng của Ubuntu khi cài đặt](#PhanVung)

<a name="LichSu"></a>
## Lịch sử phát triển 

* Linux chúng ta thường gọi tắt Linux là một hệ điều hành nhưng thực ra tên đầy đủ của Hệ điều hành chúng ta sẽ nói sau đây là GNU/Linux. Còn tên Linux chỉ là tên hạt nhân của hệ điều hành đó. Và hệ điều hành này là một ví dụ nổi tiếng nhất của phần mềm tự do và của việc phát triển mã nguồn mở.
* Phiên bản Linux đầu tiên do Linus Torvalds viết vào năm 1991,lúc ông còn là một sinh viên của trường Đại học Helsinki tại Phần Lan. 
* Ban đầu Linux được phát trển và sử dụng bởi những người say mê. Tuy nhiên, hiện nay Linux đã được các công ty lớn như IBM và Hewlett-Packard hỗ trợ, động thời nó cũng bắt kịp được các phiên bản Unix độc quyền và thậm chí là một sự thách thức lớn đối với sự thông trị của Microsoft Windown trong một số lĩnh vực.
* Tuy nhiên hiện tại phần cứng được hỗ trợ bởi Linux vẫn còn khiên tốn so với Windown. Nhưng trong tương lai số lượng phần cứng được hỗ trợ cho Linux sẽ tăng lên.
* 
<a name="Distro"></a>
## Khái niệm Distro và các distro nổi bật

* Distro (Một bản phân phối của Linux) là một hệ điều hành được tạo dựng từ tập hợp nhiều phần mềm dựa trên hạt nhân Linux và thường có một hệ thống quản lý gói tin.
* Một Distro điển hình bao gồm một Linux kernel, các công cụ và thư viện GNU, các phần mềm thêm vào, tài liệu, một Windown system, windown manager, và môi trường desktop.
* Các Distro phổ biến: Debian, Fedora, Mandriva Linux, openSUSE.
<a name="Linux"></a>
## Phân biệt Linux và Unix

* Khác biệt kỹ thuật
Unix có những đối tương khách hàng và nền tảng nhất định, và các phiên bản UNIX đều là HĐH thương mại. Các HĐH thường được phát triển có mục đích, có các tiêu chuẩn cho khách hàng và thống nhất giữa các phiên bản. 
Linux được phát triển bởi nhiều lập trình viên với bối cảnh khác nhau, vì thế có những ý kiến quan điểm và mục tiêu khác nhau
* Kiến trúc phần cứng 

Unix được lập trình để chạy trên một hoặc một nhóm kiến trúc phần cứng nhất định.
Linux chạy trên rất nhiều cấu trúc phần cứng, và số lượng các thiết bị gắn ngoài, thiếu bị I/O được sử dụng hầu như không giới hạn.

* Nhân HĐH

Các hãng phát triển Unix thường viết lại nhân HĐH, còn các hãng phát triển Linux thường sử dụng chính nhân Linux trên HĐH của mình.

* Tính mở

Unix là một HĐH đóng còn Linux là một HĐH mở.


<a name="Version"></a>
## Tìm hiểu các phiên bản của CentOS và Ubuntu

* Phiên bản của Ubuntu

Ubuntu được chia làm 2 phiên bản:
- Phiên bản hỗ trợ lâu dài (Long Term Support): Thường hỗ trợ sự cố trong 5 năm. Các phiên bản LTS thường ra mắt 2 năm 1 lần.
- Phiên bản thông thường (Standard release): Thường chỉ được hỗ trợ sự cố trong 9 tháng và luôn cập nhật các công nghệ mới.

Ubuntu đặt tên phiên bản theo 2 số cuổi của năm phát hành, và các phiên bản LTS sẽ phát hành vào năm chẵn. Và đó là phiên bản ổn định và được nhiều người sử dụng chọn.

<a name="Kernel"></a>
## Tìm hiểu Kernel, quá trình khởi động của HĐH

* Theo nghĩa hẹp, Kernet là một phần mềm quản lý tài nguyên phần cứng.


* Quá trình khởi động của hệ điều hành:

Khi bạn tao tác ấn nút nguồn trên máy tính, BIOS là chương trình chạy đầu tiên. BIOS thực hiện một công việc gọi là POST. Quá trình này sẽ kiểm tra tính sẵn sàng của phần cứng nhằm kiểm tra thông số và trạng thái của các phần cứng máy tính khác như bộ nhớ, CPU, card mạng,...
Nếu quá trình POST kết thúc thành công, thì sai đó BIOS sẽ cố gắng tìm kiếm và khởi chạy (boot) mộ hệ điều hành đwọc chứa trong các thiết bị lưu trữ như ổ cứng, CD/DVD, USB

Sau đó nó sẽ tìm đến MBR(Mastẻ Boot Record) tại sector đầu tiên của ổ đĩa cứng đầu tiên. vd /dev/hda or /dev/dsa/
MBR chứa các chỉ dẫn cho biết cách nạp trình quản lý khởi động GRUB/LILO cho Linux hay BOOTMGR cho Windows (7,8)

Boot Loader
Có 2 loại phổ biến trên Linux là GRUB và LILO
Boot loader tìm kiếm phân vùng boot và đọc thông tin cấu hình trong file grub.conf hoặc lilo.conf và hiển thị các hệ điều hành có sẵn trong máy tính cho phép chúng ta lựa chọn để khởi động, sau đó chúng sẽ nạp kernel của hệ điều hành đó vào bộ nhớ và chuyển quyền điều khiển máy tính cho kernel này.

Kernel
Sau khi chọn kernel trong file cấu hình của boot loader, hệ thống tự động nạp chương trình init trong thư mục /sbin/

Init
Tiến trình này có PID = 1, init là cha của tất cả các tiến trình khác mà có trên hệ thống Linux này. Sau đó, init đọc file /etc/inittab để xác định mức hoạt động.
