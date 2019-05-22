## Apache
* Cài đặt Apache Trên CentOS bằng gói httpd
```
yum install httpd
```
* Cài đặt Apache Trên ubuntu bằng gói apache2
```
apt-get install apache2
```
* File cấu hình
```
/etc/httpd/ (đối với centos)
/etc/apache2/ (đối với ubuntu)
```

## Nginx
* Cài đặt Nginx trên Centos
Hãy chắc chắn rằng bạn đã cài repo epel. Sau đó chỉ cần `yum install nginx` là sẽ thực hiện việc tải gói nginx về.
Nếu không làm theo các bước sau để thêm repo của nginx
    * Tạo nginx.repo
    ```
    vi /etc/yum.repos.d/nginx.repo
    ```
    Thêm vào file các dòng sau
    ```
    [nginx]
    name=nginx repo
    baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
    gpgcheck=0
    enabled=1
    ```
    * Cập nhật repo và cài đặt gói
    ```
    yum update
    yum install nginx
    ``` 
* File cấu hình của Nginx
```
/etc/nginx
```