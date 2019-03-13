# DHCP

## Overview

DHCP (Dynamic Host Configuration Protocol) là một giao thức cho phép cấp phát địa chỉ IP một cách tự động cùng với các cấu hình liên quan như subnet mask, gateway mặc định và DNS. Nó cung cấp một database trung tâm để theo dõi tất cả các máy tính trong hệ thống mạng.

DHCP là phần mở rộng của Bootstrap Protocol(BOOTP).
## Nguyên lý hoạt động

Quá trình lấy địa chỉ IP của máy trạm được mô tả như sau:

* Máy trạm khởi động với "IP rỗng" cho phép liên lạc với DHCP bằng giao thức TCP/IP. Nó chuẩn bị một thông điệp (DHCP Discover) chứa địa chỉ MAC, tên máy tính.
Thông điệp DHCP Discover có IP nguồn: 0.0.0.0;
IP đích: 255.255.255.255; IP đã từng dùng
```
IP: ID = 0x0; Proto = UDP; Len: 328
    IP: Version = 4 (0x4)
    IP: Header Length = 20 (0x14)
    IP: Service Type = 0 (0x0)
        IP: Precedence = Routine
        IP: ...0.... = Normal Delay
        IP: ....0... = Normal Throughput
        IP: .....0.. = Normal Reliability
    IP: Total Length = 328 (0x148)
    IP: Identification = 0 (0x0)
    IP: Flags Summary = 0 (0x0)
        IP: .......0 = Last fragment in datagram
        IP: ......0. = May fragment datagram if necessary
    IP: Fragment Offset = 0 (0x0) bytes
    IP: Time to Live = 128 (0x80)
    IP: Protocol = UDP - User Datagram
    IP: Checksum = 0x39A6
    IP: Source Address = 0.0.0.0
    IP: Destination Address = 255.255.255.255
    IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Discover           (xid=21274A1D)
    DHCP: Op Code           (op)     = 1 (0x1)
    DHCP: Hardware Type     (htype)  = 1 (0x1) 10Mb Ethernet
    DHCP: Hardware Address Length (hlen) = 6 (0x6)
    DHCP: Hops              (hops)   = 0 (0x0)
    DHCP: Transaction ID    (xid)    = 556223005 (0x21274A1D)
    DHCP: Seconds           (secs)   = 0 (0x0)
    DHCP: Flags             (flags)  = 0 (0x0)
        DHCP: 0............... = No Broadcast
    DHCP: Client IP Address (ciaddr) = 0.0.0.0
    DHCP: Your   IP Address (yiaddr) = 0.0.0.0
    DHCP: Server IP Address (siaddr) = 0.0.0.0
    DHCP: Relay  IP Address (giaddr) = 0.0.0.0
    DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
    DHCP: Server Host Name  (sname)  = <Blank>
    DHCP: Boot File Name    (file)   = <Blank>
    DHCP: Magic Cookie = [OK]
    DHCP: Option Field      (options)
        DHCP: DHCP Message Type      = DHCP Discover
        DHCP: Client-identifier      = (Type: 1) 08 00 2b 2e d8 5e
        DHCP: Host Name              = JUMBO-WS
        DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
        DHCP: End of this option field
```
* Mọi máy chủ DHCP có thể nhận thông điệp và chuẩn bị IP cho máy trạm. Nếu có cấu hình phù hợp nó chuẩn bị thông điệp DHCP Offer chứa địa chỉ MAC của khách, địa chỉ IP đề nghị, subnet mask, địa chỉ IP máy chủ và thời gian cho thuê. Địa chỉ đề nghị được đánh dấu "reserve". Máy chủ DHCP phát tán thông tin này trên mạng. Với IP nguồn là IP máy chủ và IP đích là 255.255.255.255
```
IP: ID = 0x3C30; Proto = UDP; Len: 328
    IP: Version = 4 (0x4)
    IP: Header Length = 20 (0x14)
    IP: Service Type = 0 (0x0)
        IP: Precedence = Routine
        IP: ...0.... = Normal Delay
        IP: ....0... = Normal Throughput
        IP: .....0.. = Normal Reliability
    IP: Total Length = 328 (0x148)
    IP: Identification = 15408 (0x3C30)
    IP: Flags Summary = 0 (0x0)
        IP: .......0 = Last fragment in datagram
        IP: ......0. = May fragment datagram if necessary
    IP: Fragment Offset = 0 (0x0) bytes
    IP: Time to Live = 128 (0x80)
    IP: Protocol = UDP - User Datagram
    IP: Checksum = 0x2FA8
    IP: Source Address = 157.54.48.151
    IP: Destination Address = 255.255.255.255
    IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Offer              (xid=21274A1D)
    DHCP: Op Code           (op)     = 2 (0x2)
    DHCP: Hardware Type     (htype)  = 1 (0x1) 10Mb Ethernet
    DHCP: Hardware Address Length (hlen) = 6 (0x6)
    DHCP: Hops              (hops)   = 0 (0x0)
    DHCP: Transaction ID    (xid)    = 556223005 (0x21274A1D)
    DHCP: Seconds           (secs)   = 0 (0x0)
    DHCP: Flags             (flags)  = 0 (0x0)
        DHCP: 0............... = No Broadcast
    DHCP: Client IP Address (ciaddr) = 0.0.0.0
    DHCP: Your   IP Address (yiaddr) = 157.54.50.5
    DHCP: Server IP Address (siaddr) = 0.0.0.0
    DHCP: Relay  IP Address (giaddr) = 0.0.0.0
    DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
    DHCP: Server Host Name  (sname)  = <Blank>
    DHCP: Boot File Name    (file)   = <Blank>
    DHCP: Magic Cookie = [OK]
    DHCP: Option Field      (options)
        DHCP: DHCP Message Type      = DHCP Offer
        DHCP: Subnet Mask            = 255.255.240.0
        DHCP: Renewal Time Value (T1) = 8 Days,  0:00:00
        DHCP: Rebinding Time Value (T2) = 14 Days,  0:00:00
        DHCP: IP Address Lease Time  = 16 Days,  0:00:00
        DHCP: Server Identifier      = 157.54.48.151
        DHCP: Router                 = 157.54.48.1
        DHCP: NetBIOS Name Service   = 157.54.16.154
        DHCP: NetBIOS Node Type      = (Length: 1) 04
        DHCP: End of this option field
```

* Khi máy trạm nhận thông điệp đề nghị và chấp nhận một trong các địa chỉ IP, máy trạm phát tán thông điệp này để khẳng định nó đã chấp nhận địa chỉ IP. (DHCP Request)
```
IP: ID = 0x100; Proto = UDP; Len: 328
    IP: Version = 4 (0x4)
    IP: Header Length = 20 (0x14)
    IP: Service Type = 0 (0x0)
        IP: Precedence = Routine
        IP: ...0.... = Normal Delay
        IP: ....0... = Normal Throughput
        IP: .....0.. = Normal Reliability
    IP: Total Length = 328 (0x148)
    IP: Identification = 256 (0x100)
    IP: Flags Summary = 0 (0x0)
        IP: .......0 = Last fragment in datagram
        IP: ......0. = May fragment datagram if necessary
    IP: Fragment Offset = 0 (0x0) bytes
    IP: Time to Live = 128 (0x80)
    IP: Protocol = UDP - User Datagram
    IP: Checksum = 0x38A6
    IP: Source Address = 0.0.0.0
    IP: Destination Address = 255.255.255.255
    IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: Request            (xid=21274A1D)
    DHCP: Op Code           (op)     = 1 (0x1)
    DHCP: Hardware Type     (htype)  = 1 (0x1) 10Mb Ethernet
    DHCP: Hardware Address Length (hlen) = 6 (0x6)
    DHCP: Hops              (hops)   = 0 (0x0)
    DHCP: Transaction ID    (xid)    = 556223005 (0x21274A1D)
    DHCP: Seconds           (secs)   = 0 (0x0)
    DHCP: Flags             (flags)  = 0 (0x0)
        DHCP: 0............... = No Broadcast
    DHCP: Client IP Address (ciaddr) = 0.0.0.0
    DHCP: Your   IP Address (yiaddr) = 0.0.0.0
    DHCP: Server IP Address (siaddr) = 0.0.0.0
    DHCP: Relay  IP Address (giaddr) = 0.0.0.0
    DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
    DHCP: Server Host Name  (sname)  = <Blank>
    DHCP: Boot File Name    (file)   = <Blank>
    DHCP: Magic Cookie = [OK]
    DHCP: Option Field      (options)
        DHCP: DHCP Message Type      = DHCP Request
        DHCP: Client-identifier      = (Type: 1) 08 00 2b 2e d8 5e
        DHCP: Requested Address      = 157.54.50.5
        DHCP: Server Identifier      = 157.54.48.151
        DHCP: Host Name              = JUMBO-WS
        DHCP: Parameter Request List = (Length: 7) 01 0f 03 2c 2e 2f 06
        DHCP: End of this option field
```
* Máy chủ phản hồi DHCP Request với DHCP Pack, hoàn tất cài đặt. Với địa chỉ nguồn vẫn là địa chỉ IP của máy chủ, địa chỉ đích là 255.255.255.255. Phần DHCP tùy chọn xác định gói là ACK
```
IP: ID = 0x3D30; Proto = UDP; Len: 328
    IP: Version = 4 (0x4)
    IP: Header Length = 20 (0x14)
    IP: Service Type = 0 (0x0)
        IP: Precedence = Routine
        IP: ...0.... = Normal Delay
        IP: ....0... = Normal Throughput
        IP: .....0.. = Normal Reliability
    IP: Total Length = 328 (0x148)
    IP: Identification = 15664 (0x3D30)
    IP: Flags Summary = 0 (0x0)
        IP: .......0 = Last fragment in datagram
        IP: ......0. = May fragment datagram if necessary
    IP: Fragment Offset = 0 (0x0) bytes
    IP: Time to Live = 128 (0x80)
    IP: Protocol = UDP - User Datagram
    IP: Checksum = 0x2EA8
    IP: Source Address = 157.54.48.151
    IP: Destination Address = 255.255.255.255
    IP: Data: Number of data bytes remaining = 308 (0x0134)

DHCP: ACK                (xid=21274A1D)
    DHCP: Op Code           (op)     = 2 (0x2)
    DHCP: Hardware Type     (htype)  = 1 (0x1) 10Mb Ethernet
    DHCP: Hardware Address Length (hlen) = 6 (0x6)
    DHCP: Hops              (hops)   = 0 (0x0)
    DHCP: Transaction ID    (xid)    = 556223005 (0x21274A1D)
    DHCP: Seconds           (secs)   = 0 (0x0)
    DHCP: Flags             (flags)  = 0 (0x0)
        DHCP: 0............... = No Broadcast
    DHCP: Client IP Address (ciaddr) = 0.0.0.0
    DHCP: Your   IP Address (yiaddr) = 157.54.50.5
    DHCP: Server IP Address (siaddr) = 0.0.0.0
    DHCP: Relay  IP Address (giaddr) = 0.0.0.0
    DHCP: Client Ethernet Address (chaddr) = 08002B2ED85E
    DHCP: Server Host Name  (sname)  = <Blank>
    DHCP: Boot File Name    (file)   = <Blank>
    DHCP: Magic Cookie = [OK]
    DHCP: Option Field      (options)
        DHCP: DHCP Message Type      = DHCP ACK
        DHCP: Renewal Time Value (T1) = 8 Days,  0:00:00
        DHCP: Rebinding Time Value (T2) = 14 Days,  0:00:00
        DHCP: IP Address Lease Time  = 16 Days,  0:00:00
        DHCP: Server Identifier      = 157.54.48.151
        DHCP: Subnet Mask            = 255.255.240.0
        DHCP: Router                 = 157.54.48.1
        DHCP: NetBIOS Name Service   = 157.54.16.154
        DHCP: NetBIOS Node Type      = (Length: 1) 04
        DHCP: End of this option field
```

Hình minh họa cho quá trình
![Hình minh họa](DHCP.png)













