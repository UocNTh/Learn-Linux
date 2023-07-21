# Tổng quan về Linux

Nội dung:

- Cấu trúc của Hệ điều hành Linux
- Ưu điểm và nhược điểm của Hệ điều hành Linux
- Tìm hiểu về Distro Linux, một số Distro phổ biến
- Giải thích: GNU/ Linux

## 1. Linux là gì?

Linux là một hệ điều hành tương tự với Microsoft Windows, nhưng Linux được tự do phát triển theo nhu cầu của người dùng

## 2. Cấu trúc của hệ điều hành Linux

Được chia làm 3 phần: 

- Kernel[1]
- Shell[2]
- Application

### 2.1. Kernel

Là một phần quan trọng của hệ điều hành, chứa các module, thư viện để quản lý và giao tiếp với phần cứng và các ứng dụng

Kernel quản lý toàn bộ hoạt động của hệ thống Linux. 

Các chức năng chính của Kernel trong hệ thống máy tính:

**Quản lý bộ nhớ**

- Cấp pháp và giải phóng bộ nhớ vật lý
- Đảm bảo mọi chương trình đều được đưa vào bộ nhớ
- Bảo vệ vùng nhớ của mỗi tiến trình

**Quản lý tiến trình**

- Kernel quản ký việc tạo, chạy và xóa mọi tiến trình.
- Lập lịch cho các tiến trình (CPU sẽ thực thi chương trình khi nào, thực thi trong bao lâu, và chương trình nào tiếp theo).
- Hỗ trợ các tiến trình có thể giao tiếp với nhau.
- Tránh xảy ra tình trạng xung đột giữa các tiến trình.

**Quản lý thiết bị**: Kernel là cầu nối giữa hệ điều hành và phần cứng

********Quản lý hệ thống file:******** Quản lý dữ liệu trên thiết bị lưu trữ (ổ cứng, thẻ nhớ)

********Quản lý mạng:******** Có nhiệm vụ quản lý các gói tin theo mô hình TCP

**System call Interface**: cung cấp các dịch vụ sử dụng phần cứng cho các tiến trình.

### 2.2 Shell

Là một chương trình, có chức năng thực thi các lệnh từ người dùng hoặc từ ứng dụng - tiện ích yêu cầu rồi chuyển đến Kernel xử lý. Shell được coi là cầu nối giữa Kernel và Application, phiên dịch các tập lệnh từ Application gửi đến Kernel để thực thi. Bản thân nó là một trình thông dịch ngôn ngữ lệnh thực thi các lệnh được đọc từ các thiết bị đầu cuối hoặc từ file. Shell được bắt đầu khi người dùng đăng nhập hoặc khởi động terminal

Một số loại shell cơ bản: 

**Bourne Shell(sh)**:

Ưu điểm: Nhỏ gọn và tốc độ → thích hợp với các lập trình viên

Nhược điểm: Thiếu các tích năng tương tác, và không có các tính năng tích hợp số học và xử lý biểu thức logic

**C Shell (csh):** 

Hỗ trợ các tính năng lập trình vô cùng tiện lợi (số học tích hợp và cú pháp biểu thức C-like), có các tính năng kết hợp sử dụng tương tác (bí danh và lịch sử lệnh)

**Korn Shell (ksh):**

Có các tính năng tương đương với csh, nhanh hơn csh, và chạy được các script được viết cho sh

****GNU Bourne-Again Shell (bash):****

Tương thích với sh, tích hợp các tính năng hữu ích từ ksh và csh, có các phím mũi tên cho phép tự động map để recall lệnh và chỉnh sửa

Câu lệnh kiểm tra các shell đang có trên hệ thống: cat /etc/shells

Câu lệnh kiểm tra shell đang dùng: echo $0

### 2.3 Applications

Là các ứng dụng và tiện ích mà người dùng cài đặt trên Server. VD: ftp, Proxy

## 3. Ưu điểm và nhược điểm của Hệ điều hành Linux

**Ưu điểm**: 

- Bản quyền và chi phí: Linux là hệ điều hành miễn phí và mã nguồn mở (open source). Bên cạnh đó Linux còn miễn phí tất cả các tính năng đi kèm, bộ ứng dụng văn phòng đi kèm nên không lo ngại về vấn đề bản quyền
- Bảo mật: Rất ít virus trên Linux tồn tại. Một hacker sẽ khó có thể dành thời gian phát triển phần mềm độc hại cho một hệ điều hành chiếm ít phần trăm thị trường máy tính để bàn (năm 2020 chiếm 3.17%). Nguyên nhân tiếp theo là người dùng Linux thường có kiến thức cơ bản về hệ điều hành này nên tránh được rất nhiều phần mềm độc hại. Linux quản lý người dùng rất chặt chẽ (phân quyền người dùng). Ở Windows, người dùng thường có quyền làm mọi thứ liên quan tới hệ thống (có thể vào thư mục của hệ thống và xóa mọi thứ trong đó → ảnh hưởng rất nhiều đến hệ điều hành) và Linux không cho phép điều đó, bất kỳ các hoạt động liên quan đến hệ điều hành, Linux sẽ yêu cầu mật khẩu của nhà quản trị hệ thống, và virus không thể tự do xóa mọi thứ trong máy vì chúng không có quyền.
- Linh hoạt: Người dùng có thể thực hiện các tùy chỉnh
- Chạy ổn định trên các máy tính có cấu hình yếu: Chạy mượt mà, độ ổn định cao trên các máy có cấu hình thấp và được nâng cấp, hỗ trợ thường xuyên từ nhà phát hành

********Nhược điểm:********

- Số lượng ứng dụng hỗ trợ vẫn còn rất hạn chế
- Một số nhà sản xuất không phát triển driver hỗ trợ nền tảng Linux.
- Mất thời gian để làm quen, đặc biệt là khi chuyển từ Windows sang sử dụng Linux thì sẽ cần thời gian để sử dụng

## 4. Các phiên bản Distro Linux

Hệ điều hành mở cho phép người dùng sử dụng miễn phí, tự do phát triển và định hướng hay tùy chỉnh theo nhu cầu thực tế của mình (được gọi là Distro Linux) → đây là một điều khó có thể làm được ở các hệ điều hành đóng

Các phiên bản Distro Linux[3] sẽ hướng đến một nhóm đối tượng và phục vụ nhu cầu sử dụng khác nhau. 

Giống nhau: 

- Tất cả đều dựa trên 3 nhánh chính: Debian, Red Hat, Slackware
- Tất cả các Distro Linux đều có Kernel và Linux

Khác nhau: 

**Xét về thị trường:** 

- Nhóm 1: **Gentoo và Slackware**
    
    Các các bản distro linux này nhắm vào người dùng am hiểu Linux. Do đó, phần lớn các phương thức xây dựng, cũng như cấu hình của hệ thống được thực hiện qua dòng lệnh.
    
- Nhóm 2: **Debian, Fedora**
    
    Đối tượng người dùng của nhóm 2 là người am hiểu về hệ thống nhưng chưa thực sự hiểu về Linux. Vì vậy, distro sẽ cung cấp cho họ nhiều công cụ hơn. Nhóm này phù hợp với người dùng mới bắt đầu sử dụng Linux.
    
    Các distro của nhóm 2 lại có quy trình phát triển và kiểm tra chất lượng phần mềm khắt khe hơn các nhóm còn lại. Do đó, để trở thành lập trình viên chính thức của nhóm này, cần phải có thời gian đóng góp dài. Đồng thời, được chứng nhận chất lượng bởi những lập trình viên khác. Do đó, giới công nghệ luôn đánh giá cao môi trường của nhóm Debian, Fedora.
    
- Nhóm 3: **Centos**, **RHEL**, **SUSE EL**
    
    Nhắm vào thị thường máy chủ, doanh nghiệp, cơ quan,...Vì chúng có sự ổn định cao, thời gian ra phiên bản mới lâu (3-5 năm), Ngoài ra còn có các dịch vụ hỗ trợ thương mại.
    
- Nhóm 4: **Ubuntu**, **Open SUSE**, **Linux Mint**
    
    Nhắm vào người mới bắt đầu dùng Linux và người dùng cuối. Gồm các đặc tính: phát triển trong thờ gian ngắn, ứng dụng các công nghệ mới liên tục, nhiều công cụ đồ họa thiết kế và cấu hình hệ thống theo nhu cầu sử dụng.
    

**Xét về triết lý phần mềm:**

- Nhóm 1: Có cấu trúc gọn, linh hoạt để các lập trình viên có thể xây dựng theo nhu cầu của mình.
- Nhóm 2: Nhắm đến sự chuẩn hóa quá trình phát triển phần mềm, nhằm tạo ra hệ thống hoạt động nhịp nhàng và hạn chế tối đa lỗ hổng bảo mật.
- Nhóm 3: Phát triển theo hướng bền vững, chuyên nghiệp, phù hợp cho việc cung cấp sản phẩm/dịch vụ dài hạn, có vòng đời lên tới 7 năm.
- Nhóm 4: Đi theo hướng công nghệ. Nhóm này có công cụ hiệu ứng đồ họa và không cần chỉnh nhiều.

## 5. GNU/Linux

Một hệ điều hành gồm có nhiều chương trình cơ bản khác nhau do máy tính cần thiết để liên lạc với và nhận lệnh từ người dùng; đọc từ và ghi vào đĩa cứng, băng và máy in; điều khiển cách sử dụng bộ nhớ; chạy phần mềm khác. Trong hệ điều hành, phần quan trọng nhất là hạt nhân. Trong hệ thống kiểu GNU/LInux, Linux là thành phần hạt nhân. Phần còn lại của hệ thống chứa chương trình khác nhau, gồm nhiều phần mềm do dự án GNU (**GNU’s Not Unix)** ghi hay hỗ trợ. Vì vậy hệ điều hành được gọi là GNU/Linux[4].

---

Nguồn tham khảo: 

[[1] Tìm hiểu thêm về Linux Kernel](https://vimentor.com/en/lesson/gioi-thieu-ve-linux-kernel-1)

[[2] Shell là gì? 4 loại shell phổ biến](https://bizflycloud.vn/tin-tuc/shell-la-gi-20181119092604977.htm)

[[3] Distro Linux là gì? Nên dùng Distro Linux nào, sự khác nhau?](https://hostingviet.vn/distro-linux-la-gi)

[[4] Lịch sử hình thành của Linux? Giải thích tên gọi GNU/Linux](https://blog.cloud365.vn/other/lich-su-hinh-thanh-linux/)