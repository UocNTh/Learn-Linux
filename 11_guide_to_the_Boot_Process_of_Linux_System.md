# Guide to the Boot Process of Linux System

![https://www.baeldung.com/wp-content/uploads/sites/2/2022/10/boot-process-662x1024.png](https://www.baeldung.com/wp-content/uploads/sites/2/2022/10/boot-process-662x1024.png)

**BIOS (Basic Input Output System) / UEFI (Unified Extensible Firmware Interface)**

Từ khóa cần tìm hiểu: 

- Firmware
- Drive

Giải thích từ khóa: 

**Firmware**: là một chương trình phần mềm dùng để kiểm soát và điều khiển phần cứng của các thiết bị điện tử: máy tính, điện thoại. 

Một số loại fireware: BIOS và UEFI 

Khi bật máy tính, firmware, chẳng hạn như BIOS hoặc UEFI sẽ được kích hoạt đầu tiên. nó sẽ thực hiện các bước khởi động như kiểm tra phần cứng, tải hệ điều hành, chuẩn bị hệ thống để chạy các ứng dụng và chương trình khác

Sau khi firmware đã kiểm tra xong thì nó sẽ tài hệ điều hành từ ổ cứng, chuyển quyền kiểm soát máy tính sang cho hệ điều hành. Sau đó thì hệ điều hành sẽ quản lý các hoạt động của máy tình trong thời gian sử dụng,

Khi tắt máy tính thì hệ điều hành sẽ gửi thông báo đến cho firmware, firmware sẽ thực hiện tắt máy tính mỗ cách an toàn 

**Drive:** Máy tính có 2 phần cơ bản: Phần cứng và phần mềm. Để kết nối phần cứng và phần mềm thì cần một cầu nối. Cầu nối này gọi là “**drive**”. Là môi trường giúp cho hệ điều hành tương tác được với các thiết bị phần cứng. VD: Audio Drive: kết nối hệ điều hành với loa. LAN Drive: hỗ trợ cho mạng dây. Wireless Drive: giúp máy tính kết nối với Wifi hoạt động tốt

---

Chương trình BIOS hoặc UEFI được khởi động sau khi hệ thống bật nguồn. BIOS chứa các mã code để có quyền truy cập ban đầu vào các thiết bị: 

- Bàn phím
- Màn hình
- Ổ đĩa

Hầu hết các thiết bị sẽ có một trình điều khiển thiết bị chuyên dụng sau khi hệ thống khởi động hoàn toàn. 

Sau đó,  BIOS hoặc UEFI chạy POST (Power-on Seft Test). POST thực hiện các task:

- Xác minh phần cứng và các thiết bị ngoại vi
- Đảm bảo máy tính hoạt động tốt

Nếu trong quá trình kiểm tra, phát hiện lỗi thì sẽ hiển thị trên màn hình. Nếu không phát hiện thấy RAM, POST sẽ kích hoạt tiếng bíp.

Nếu kiểm tra thành công thì tiến hành các giai đoạn tiếp theo

Tiếp theo, sau khi kiểm tra thành công. BIOS hoặc UEFI sẽ chọn những boot device theo thứ tự (có thể chính sửa thứ tự)

- Ổ đĩa
- USB
- CD

Với BIOS thì nó sẽ có boot loader nằm ở sector đầu tiên của boot device. 

Boot loader là một chương trình nhỏ tải hệ điều hành. Công việc chính của trình tải khởi động là thực hiện ba hành động với hạt nhân: định vị trên đĩa, chèn vào bộ nhớ và thực hiện với các tùy chọn được cung cấp.

Các hoạt động của Grub:

- Tiếp quản từ BIOS hoặc UEFI tại thời điểm khởi động
- Tải
- Chèn nhân Linux vào bộ nhớ
- Chuyển việc thực thi sang kernel

Sau khi thông qua BIOS hoặc UEFI, POST và sử dụng trình  boot loader để khởi động kernel, hệ điều hành hiện kiểm soát quyền truy cập vào tài nguyên máy tính

Ở đây, Linux kernel tuân theo một quy trình được xác định trước:

- Tự giải nén tại chỗ
- Thực hiện kiểm tra phần cứng
- Có quyền truy cập vào phầm cứng và các thiết bị ngoại vi
- Chạy tiến trình init ( chạy các file init script oẻ trong thư mục /etc/init.d )

**Systemd**

Kernel bắt đầu tiến trình init, bắt đầu tiến trình cha. Ở đây, cha của tất cả các tiến trình Linux là Systemd. Làm theo các bước khởi động, Systemd thực hiện một loạt các tác vụ:

- Thăm dò tất cả phần cứng còn lại
- Gắn kết hệ thống tập tin
- Bắt đầu và chấm dứt các dịch vụ
- Quản lý các tiến trình hệ thống thiết yếu như đăng nhập người dùng
- Chạy một môi trường máy tính

Thật vậy, những nhiệm vụ này và các nhiệm vụ khác cho phép người dùng tương tác với hệ thống. 

**Run Levels**

Cấp độ chạy (run levels) trong Linux được sử dụng để quản lý trạng thái hoạt động của hệ thống. Mỗi cấp độ chạy đại diện cho một tình trạng cụ thể của hệ thống, xác định các dịch vụ và tiến trình đang chạy.

Các cấp độ chạy có mục đích khác nhau và hữu ích trong nhiều tình huống:

1. Halt (cấp độ 0): Dừng hệ thống, tắt máy. Sử dụng khi bạn muốn tắt hoàn toàn hệ thống.
2. Single-user mode (cấp độ 1): Chế độ đơn người dùng, sử dụng cho bảo trì và khắc phục sự cố. Thường chỉ có một phiên làm việc duy nhất cho người dùng root.
3. Multi-user mode with networking (cấp độ 3): Chế độ đa người dùng có mạng. Đây là cấp độ mặc định cho nhiều hệ thống Linux, chạy dịch vụ mạng và cho phép nhiều người dùng đăng nhập cùng một lúc.
4. Multi-user mode with networking and GUI (cấp độ 5): Chế độ đa người dùng có mạng và giao diện người dùng đồ họa (GUI). Thường được sử dụng khi bạn muốn hệ thống khởi động vào môi trường đồ họa với các dịch vụ mạng đã được kích hoạt.
5. Reboot (cấp độ 6): Khởi động lại hệ thống. Sử dụng khi bạn muốn khởi động lại máy tính một cách an toàn.

Bằng cách chuyển đổi giữa các cấp độ chạy, người dùng có thể quản lý các tác vụ khác nhau như khởi động, tắt máy, hoặc thực hiện các công việc bảo trì, sửa chữa, và kiểm tra lỗi.

---

**Phân biệt tiến trình init và Systemd (init system)??**

1. Tiến trình init: Là tiến trình đầu tiên (thường có số PID là 1) trong hệ thống Linux. Nhiệm vụ chính của tiến trình init là khởi động các tiến trình và dịch vụ cần thiết để hệ thống hoạt động. Trong các phiên bản Linux truyền thống, tiến trình init có thể được triển khai bằng các hệ thống init như SysVinit hoặc Upstart.
2. Systemd: Là một hệ thống init mới và phổ biến trong hệ điều hành Linux. Nó không phải là một tiến trình, mà là một phần mềm, một init system. Systemd có chức năng quản lý tiến trình và dịch vụ như một tiến trình init, nhưng nó cũng bao gồm các tính năng mạnh mẽ hơn như quản lý các "units" (đơn vị) của hệ thống, giám sát, tự động khởi động lại dịch vụ khi cần thiết và nhiều tính năng nâng cao khác.

Tóm lại, tiến trình init là tiến trình đầu tiên trong hệ thống, còn Systemd là một hệ thống init hiện đại và mạnh mẽ dùng để quản lý tiến trình và dịch vụ cũng như nhiều tính năng hỗ trợ khác.
