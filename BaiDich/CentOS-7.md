# CentOS 7
Ghi lại một số điều chỉnh của bạn trong CentOS. Một bản ghi hoạt động khi khởi tạo.

## Hệ thống
Đây là thay đổi lớn nhất trong CentOS 7, vì vậy bạn cần có thời gian để làm quen với nó.
Tất cả các dịch vụ
```
systemctl list-units --type service
```
Service start
```
systemctl list-unit-files --type=service | grep enabled
```
Các lệnh với một service
```
# systemctl status <name>
# systemctl stop <name>
# systemctl disable <name>
# systemctl start <name>
# systemctl restart <name>
```
`https://www.rayheffer.com/essential-linux-skills-with-centos-7-managing-services-with-systemd/`

## Chrony service
CentOS 7 thực sự khuyên bạn nên sử dụng dịch vụ chrony để đạt được thời gian đồng bộ hóa. Tôi đã sử dụng cài đặt tối thiểu của CentOS 7, dịch vụ Chrony chưa được cài đặt.
```
yum install chrony
systemctl start chronyd
systemctl enable chronyd
```
Máy chủ thời gian đồng bộ hóa mặc định là CentOS, bạn có thể sửa đổi nó thành máy chủ thời gian trong khu vực.
`vi /etc/chrony.conf`
```
server 0.cn.pool.ntp.org iburst
server 1.cn.pool.ntp.org iburst
server 2.cn.pool.ntp.org iburst
server 3.cn.pool.ntp.org iburst
```
Ngay sau đó, khởi động lại dịch vụ chronyd
```
systemctl restart chronyd
chronyc sources
```
Lần này bạn sẽ tìm thấy một máy chủ thời gian trong nước. Lưu ý rằng nếu thời gian máy và thời gian tiêu chuẩn của bạn khác nhau, bạn cần buộc đồng bộ hóa. Dừng dịch vụ chrony trước khi bạn buộc thời gian đồng bộ hóa.
```
systemctl stop chronyd
chronyd -q 'pool pool.ntp.org iburst'
```
Sau thời gian đồng bộ hóa bắt buộc, hãy bắt đầu lại với dịch vụ chrony. Tài liệu của Red Hat là tài liệu tốt nhất và chính xác nhất thế giời.
`https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/sect-using_chrony`

```
chronyc tracking
chronyc sources
chronyc sourcestats
```
## Date and Time
Xem thời gian và múi giờ hiện tại.
```
# timedatectl status
      Local time: Tue 2017-12-12 18:02:46 CST
  Universal time: Tue 2017-12-12 10:02:46 UTC
        RTC time: Tue 2017-12-12 10:02:46
       Time zone: Asia/Shanghai (CST, +0800)
     NTP enabled: yes
NTP synchronized: yes
 RTC in local TZ: no
      DST active: n/a
```
Nếu bạn muốn tự sửa đổi thời gian, lần này, trước tiên bạn cần dừng thời gian đồng bộ hóa.
```
timedatectl set-ntp 0
```
Tại thời điểm này bạn có thiết lập thời gian
```
timedatectl set-time 17:00:00
```
Nếu dịch vụ `ntp` được kích hoạt
```
timedatectl set-ntp 1
```
Sửa đổi ngày
```
timedatectl set-time ‘YYYY-MM-DD  HH:MM:SS’
```
Xem thời gian phần cứng
```
hwclock
```
Đồng bộ hóa thời gian `system` với phần cứng
```
hwclock --hctosys
```
`http://linuxtechlab.com/playing-date-time-rhelcentos/`

## Tìm kiếm
Việc tìm kiếm thường sẽ xảy ra thấy thường xuyên với người dùng hệ thống CentOS

```
find /etc -name "yum.*" -type f
```
Với nhiều option như `-type f` tìm file, `-type d` tìm kiếm thư mục.

* Một cách đơn giản khác là cài đặt gói mlocate, bạn có thể tìm kiếm trực tiếp
```
yum install mlocate
```
Cập nhật cơ sở dữ liệu
```
updatedb
# locate yum.conf
/etc/yum.conf
/usr/share/man/man5/yum.conf.5
```
Phương pháp này thực sự không được khuyến khích, hoặc tốt hơn là sử dụng find.

* Xem tập tin gói nào thuộc về `rpm`
```
# rpm -qf /etc/yum.conf
yum-3.4.3-154.el7.centos.noarch
```
Kiểm tra những tập tin liên quan đến gói rpm đó khi cài đặt.
```
 rpm -ql chrony
/etc/NetworkManager/dispatcher.d/20-chrony
/etc/chrony.conf
/etc/chrony.keys
```
* Nếu cần tìm kiếm từ khóa
```
grep -rlw "tecadmin" /var/log
```
Thêm tham số `-i` để tìm kiếm không phân biệt chữ hoa chữ thường.
`https://tecadmin.net/find-all-files-containing-specific-text-on-linux/`

## Phiên bản kernel

Xem phiên bản hệ điều hành
```
cat /etc/redhat-release
CentOS Linux release 7.4.1708 (Core)
```
Kiểm tra phiên bản kernel
```
# uname -a
Linux server01.chenshake.com 3.10.0-693.el7.x86_64

#1 SMP Tue Aug 22 21:09:27 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```
Trước đây số phiên bản của kernel rất khó nhớ nhưng bây giờ đã được thêm thời gian. Phiên bản kernel này là phiển bản kernel mặc định cho centos 7.4. Nếu nâng cấp bạn sẽ thấy phiên bản mới nhất là
```
]# uname -a
Linux server01.chenshake.com 3.10.0-693.11.1.el7.x86_64

#1 SMP Mon Dec 4 23:52:40 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
```
## Nâng cấp
Cập nhật gói hệ thống
```
yum update
```
Nó có thể khiến kernel được nâng cấp và yêu cầu khởi động lại để có hiệu lực.
Nâng cấp phiên bản hệ điều hành, ví dụ 7.3 lên 7.4
```
yum upgrade
```
## vim

```
yum install vim
```
Chỉnh sửa file /etc/profile
```
# add at the last line
alias vi='vim'
```
Để các cài đặt có hiệu lực ngay lập tức
```
source /etc/profile
```
Theo mặc định, vim của CentOS 7 đã hỗ trợ khả năng khôi phục về vị trí con trỏ cuối cùng, có thể được sử dụng mà không cần điều chỉnh. Chỉnh sửa tệp /etc/vimrc nếu bạn cần sửa đổi cấu hình.
```
set ignorecase
```
Tôi bỏ qua trường hợp khi tôi tăng tìm kiếm

## Selinux
Đó là một cách phổ biến để tắt selinux, bao gồm kiểm tra xem selinux có bị đóng không.
```
# sestatus
SELinux status:                 enabled
```
Đóng Selinux
```
sed -i 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config
setenforce 0
```
Thói quen của tôi là khởi động lại máy, để đảm bảo hiệu quả.
```
# sestatus
SELinux status:                 disabled
```

## Cài đặt Repo
Để thuận tiện, tốt nhất là cài đặt bộ Red Hat yum

Xem repo
```
cd /etc/yum.repos.d/
mkdir backup
move CentOS* ./backup/
```
Thiết lập nguồn Ali
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```
Kiểm tra
```
yum clean all
yum makecache
yum list | wc -l
```
Nếu chúng tôi muốn thêm repo docker, bạn có thể sử dụng phương pháp này.
```
yum-config-manager \
--add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

## lrzsz
Công cụ này thực sự rất tiện lợi dưới xshell, tài lên và tải xuống các tệp.
```
yum install lrzsz
```
## Tắt tường lửa
```
systemctl status firewalld
systemctl disable firewalld.service
systemctl stop firewalld.service
```
## Tên máy chủ
Cần tìm ra sự khác biệt giữa hostname và FQDN Name

* Cài đặt hostname
```
# cat /etc/hostname
server01
```
Nếu muốn sửa đổi nó, bạn có thể sử dụng lệnh
```
hostnamectl –static set-hostname server01
```
Để những thay đổi có hiệu lực ngay lập tức
```
hostname -F /etc/hostname
```
* Cài đặt FQDN
```
# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.100.10	server01.chenshake.com	server01
```
Xem
```
# hostname
server01

hostname -f
server01.chenshake.com
```
-f có nghĩa là FQDN, tương tự như tên của tên miền

Thông qua hostnamectl, bạn cũng có thể kiểm tra trạng thái chung của hệ thống, cho dù đó là máy VM hay máy vật lý
```
# hostnamectl status
   Static hostname: server01
         Icon name: computer-vm
           Chassis: vm
        Machine ID: 7c4bea6eadac4a1cae068a167a0c961b
           Boot ID: 173cfb58e1c948ce947bd8261b327f91
    Virtualization: vmware
  Operating System: CentOS Linux 7 (Core)
       CPE OS Name: cpe:/o:centos:centos:7
            Kernel: Linux 3.10.0-693.11.1.el7.x86_64
      Architecture: x86-64
```

## Công cụ mạng
Một số công cụ mạng phổ biến cần được cài đặt.

1. netstat, cần cài đặt net-tools
2. nmap, cần cài đặt nmap
3. lsof, cần cài đặt lsof

```
yum install net-tools lsof nmap
```
Sử dụng
```
netstat -nlptu
```
Một số option cần biết
    * `-n` Cho biết ip thành tên miền không được giải quyết, tham số này phải là
    * `-l` Cho biết hiển thị cổng mở
    * `-p` Cho biết tên ứng dụng cổng
    * `-t` đại diện cho giao thức TCP
    * `-u` đại diện cho giao thức UDP

Xem điều kiện cổng 22
```
lsof -i :22
```
lsof rất mạnh mẽ, bao gồm kiểm tra nếu một tệp đang được sử dụng bởi một quy trình.
```
lsof /usr/sbin/sshd
```
nmap thực sự là một công cụ quét, tự quét và nhìn vào cổng.
```
nmap localhost
```
`https://www.cyberciti.biz/faq/howto-install-nmap-on-centos-rhel-redhat-enterprise-linux/`

## Đóng IPv6
Chỉnh sửa /etc/sysctl.conf
```
net.ipv6.conf.all.disable_ipv6 = 1
```
Áp dụng ngay lập tức
```
sysctl -p
```

So sánh
* Trước khi đóng cổng
```
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:0c:29:9e:48:a3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.10/24 brd 192.168.100.255 scope global ens33
       valid_lft forever preferred_lft forever
    inet6 fe80::7a67:a172:a8cd:635/64 scope link
       valid_lft forever preferred_lft forever
```
* Sau khi đóng cổng
```
# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP qlen 1000
    link/ether 00:0c:29:9e:48:a3 brd ff:ff:ff:ff:ff:ff
    inet 192.168.100.10/24 brd 192.168.100.255 scope global ens33
       valid_lft forever preferred_lft forever
```
`http://aws-labs.com/disable-ipv6-centos-7-rhel-7/`

## Số lượng tệp mở tối đa
Nội dung sau đây không được hiển thị đầy đủ

Trong quá trình phát triển vận hành và bảo trì, chúng ta thường gặp phải "Ổ cắm/ Têp: Không thể mở nhiều tệp", "không thể mở thêm quy trình", lần này, chúng ta cần điều chỉnh các tham số mặc định của hệ thống.

### file-max
Số lượng tệp tối đa mà kernel có thể phân bố
```
# cat /proc/sys/fs/file-max
396334
```
Số lượng mô tả tệp mở tối đa trong hệ thống
```
cat /proc/sys/fs/file-nr
960	0	396334
```
Sửa đổi tạm thời
```
echo 1000000 > /proc/sys/fs/file-max
```
Sửa đổi vĩnh viễn được đặt trong /etc/sysctl.conf
```
fs.file-max = 1000000
```
Số lượng mô tả tệp mở tối đa cho một quy trình, nr_open là số lượng tệp tối đa mà một quy trình có thể phân bố.

* soft link
```
# ulimit -n
1024
```
* hard link
```
# ulimit -Hn
4096
```

Sửa đổi

<http://blog.csdn.net/superchanon/article/details/13303705>

<http://blog.51cto.com/qujunorz/1703295>

<https://unix.stackexchange.com/questions/127777/how-to-configure-the-process-open-file-limit-of-a-user>




