## 1. Giới thiệu về ảo hóa
Công nghệ truyền thống sử dụng mối quan hệ 1:1 tồn tại giữa máy chủ vật lý và hệ điều hành. Mối quan hệ này sử dụng ít công suất, chỉ khoảng 5-10% công suất của máy chủ vật lý. Muốn triển khai nhiều hệ điều hành phải có nhiều máy chủ vật lý, mỗi lần nâng cấp phần cứng mất nhiều thời gian, kinh phí.

Mô hình phổ thông này không linh hoạt và có nhiều chi phí phát sinh như chi phí đầu tư, không gian, điện năng tiêu thụ, hệ thống làm mát, chi phí bảo trì...

Công nghệ ảo hóa là một công nghệ được ra đời nhằm khai thác triệt để khả năng làm việc của một máy chủ vật lý. Ảo hóa cho phép vận hành nhiều máy ảo trên cùng một máy chủ vật lý, dùng chung các tài nguyên của một máy chủ vật lý như CPU, Ram, ổ cứng,… và các tài nguyên khác. Các máy ảo khác nhau có thể vận hành hệ điều hành và ứng dụng trên cùng một máy chủ vật lý.

## 2. Chức năng và Lợi ích
* Chức năng:
    * Phân chia: Có thể chia từ một máy vật lý thành nhiều máy ảo với nhiều hệ điều hành khác nhau
    * Cô lập: Ví dụ Một dịch vụ quan trọng chạy trên một máy ảo, nếu máy ảo đó gặp trục trặc thì không ảnh hưởng đến các dịch vụ khác
    * Đóng gói: Có thể dễ dàng đóng gói sao chép để backup di chuyển sang các môi trường khác.

* Lợi ích: Ảo hóa giúp giảm chi phí trong khi đó lại tăng hiệu quả, tính linh động. Giảm số lượng máy chủ, giảm điện năng tiêu thụ, tiết kiệm chi phí cho việc bảo trì phần cứng. Nâng cao hiệu quả công việc.
Dễ dàng mở rộng hệ thống khi có nhu cầu, triển khai máy chủ ảo nhanh, tận dụng tài nguyên hiện có.
Khai thác triệt để các tài nguyên của phần cứng vật lý bằng cách chạy nhiều hệ điều hành trên mạng một chủ vật lý.
