# File System

Nội dung:

- Cấu trúc thư mục trong linux, ý nghĩa các thư mục chính
- Các loại file system linux (ví dụ EXT2, EXT3, EXT4, XFS,…)
- Phân biệt đường dẫn tuyệt đối và đương dẫn tương đối
- Các lệnh để di chuyển qua các thư mục (`cd` )
- Các option với lệnh `ls`

## 1. Cấu trúc thư mục trong Linux, ý nghĩa của thư mục chính

![https://media.geeksforgeeks.org/wp-content/uploads/20230516105759/151.webp](https://media.geeksforgeeks.org/wp-content/uploads/20230516105759/151.webp)

**/**

- Thư mục gốc root. Mọi file và thư mục đều bắt đầu từ thư mục gốc. Người dùng root duy nhất có quyền ghi vào thư mục này. Cần phân biết ****/**** và ******/root******

********/bin********

- Chức các file  thực thi nhị phân. Các lệnh Linux phổ biến mà cần sử dụng trong chế độ một người dùng. Các lệnh được sử dụng bởi tất cả người dùng hệ thống
- VD: ps, ls, cat

******/boot****** 

- Lưu trữ các file cần thiết để Linux khởi động

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/boot.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/boot.png?raw=true)

********/dev********

- Các file thiết bị cần thiết - nơi lưu trữ các phân vùng ổ cứng, thiết bị ngoại vi như usb hoặc bất cứ thiết bị nào được cắm vào hệ thống

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/dev.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/dev.png?raw=true)

********/etc******** 

- Các file cấu hình cho các chương trình hoạt động. Thường là những tệp tin dạng text thường.

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/etc.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/etc.png?raw=true)

************/home************ 

- Thư mục chính của người dùng, chứa các tệp đã lưu cài đặt cá nhân

**/lib** 

- Chứa các tập tin thư viện để hỗ trợ các tập tin thực thi được lưu trong */bin* và */sbin*

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/lib.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/lib.png?raw=true)

******/lost+found****** 

- Trên Linux, người dùng sử dụng lệnh **fsck** (file system check) để kiểm tra các tập tin hệ thống bị lỗi **fsck** có thể tìm thấy các tập tin bị lỗi trên hệ thống tập tin. Nếu phát hiện có bất kỳ tập tin nào bị lỗi, fsck sẽ loại bỏ dữ liệu bị lỗi từ hệ thống tập tin và di chuyển vào thư mục lost+found.
- Giả sử nếu tắt máy tính đột ngột khi máy tính đang chạy và các tập tin đang được ghi vào ổ đĩa cứng, công cụ fsck sẽ tự động kiểm tra các tập tin hệ thống của bạn trong lần khởi động máy tính tiếp theo. Nếu có bất kỳ dữ liệu nào bị lỗi, nó sẽ cho vào thư mục lost+found.

**************/media************** 

- Trong hệ điều hành Linux, thư mục "/media" là một thư mục được sử dụng để gắn kết các thiết bị lưu trữ tạm thời, chẳng hạn như ổ đĩa USB, ổ đĩa CD/DVD, thẻ nhớ, ổ đĩa cứng ngoài, và các thiết bị lưu trữ di động khác. Khi cắm một thiết bị lưu trữ vào máy tính, hệ điều hành Linux sẽ thường tự động gắn kết nó vào thư mục "/media".
- Khi thiết bị được gắn kết vào thư mục "/media", người dùng có thể truy cập vào nó và làm việc với dữ liệu trong đó giống như làm việc với bất kỳ thư mục nào khác trên hệ thống tệp tin.

**********/mnt (mount directory)**********

- Thư mục "/mnt" được sử dụng để gắn kết các thiết bị lưu trữ tạm thời hoặc các thiết bị lưu trữ dài hạn (ví dụ như các ổ đĩa chia sẻ mạng) một cách thủ công bởi người dùng hoặc quản trị viên hệ thống. Trong khi thư mục "/media" thường được sử dụng cho các thiết bị tạm thời tự động gắn kết, thư mục "/mnt" có thể được sử dụng cho các thiết bị lưu trữ dài hạn hoặc các thiết bị cần gắn kết thủ công.
- Người dùng hoặc quản trị viên hệ thống phải tự gắn kết các thiết bị vào thư mục "/mnt" bằng cách sử dụng lệnh "mount".

************/opt************  

- Các gói phần mềm ứng dụng tùy chọn. Chứa các ứng dụng bổ sung từ các nhà cung cấp riêng lẻ. Các ứng dụng bổ sung nên được cài đặt trong thư mục con /opt/ hoặc /opt/.

**/sbin**  

- Các nhị phân hệ thống cần thiết, ví dụ: fsck, init, route. Giống như /bin, /sbin cũng chứa các tệp thực thi nhị phân. Các lệnh linux nằm trong thư mục này thường được quản trị viên hệ thống sử dụng cho mục đích bảo trì hệ thống.

**/srv**  

- Chứa dữ liệu liên quan đến các dịch vụ máy chủ như /srv/svs, chứa các dữ liệu liên quan đến CVS.

************/tmp************  

- Thư mục chứa các tệp tạm thời được tạo bởi hệ thống và người dùng. Các tệp trong thư mục này sẽ bị xóa khi khởi động lại hệ thống.

**/usr**  

Hệ thống phân cấp phụ cho dữ liệu người dùng chỉ đọc; chứa phần lớn các tiện ích và ứng dụng (nhiều) người dùng.

- Chứa các tệp nhị phân, thư viện, tài liệu và mã nguồn cho các chương trình cấp hai.
- /usr/bin chứa các tệp nhị phân cho chương trình người dùng. Nếu bạn không thể tìm thấy mã nhị phân người dùng trong /bin, hãy xem trong /usr/bin. Ví dụ: at, awk, cc, less, scp
- /usr/sbin chứa các tệp nhị phân dành cho quản trị viên hệ thống. Nếu bạn không thể tìm thấy nhị phân hệ thống trong /sbin, hãy xem trong /usr/sbin. Ví dụ: atd, cron, sshd, useradd, userdel
- /usr/lib chứa các thư viện cho /usr/bin và /usr/sbin
- /usr/local chứa các chương trình của người dùng mà bạn cài đặt từ nguồn. Ví dụ: khi bạn cài đặt apache từ nguồn, nó sẽ nằm trong /usr/local/apache2
- /usr/src chứa các nguồn nhân Linux, tệp tiêu đề và tài liệu.

**************/proc**************  

- Lưu các thông tin về tình trạng của hệ thống

---

## 2. Các loại file system linux

***journaling là gì?**  Được sử dụng khi ghi dữ liệu lên ổ cứng và đóng vai trò như những chiếc đục lỗ để ghi thông tin vào phân vùng. Đồng thời, nó cũng khắc phục vấn đề xảy ra khi ổ cứng gặp lỗi trong quá trình này, nếu không có journal thì hệ điều hành sẽ không thể biết được file dữ liệu có được ghi đầy đủ tới ổ cứng hay chưa.*

**Ext - Extended file system**: là định dạng file hệ thống đầu tiền được thiết kế để hỗ trợ cho nhân Linux. Phiên bản Ext đầu tiên là phần được nâng cấp từ file hệ thống Minix. Hiện tại ít được sử dụng do không đáp ứng được nhiều những tính năng phổ biến ngày nay.

**Ext2** được kế thừa các thuộc tính của file hệ thống cũ, đồng thời hỗ trợ dung lượng ổ cứng lên đến 2TB. Ext2 không sử dụng journal cho nên sẽ có ít dữ liệu được lưu vào ổ đĩa hơn. Do lượng yêu cầu viết và xóa dữ liệu khá thấp, cho nên rất phù hợp với những thiết bị lưu trữ bên ngoài như thẻ nhớ, ổ USB...

**Ext3** về căn bản chỉ là **Ext2** đi kèm với journaling. Mục đích chính của **Ext3** là tương thích ngược với **Ext2**, và do vậy những ổ đĩa, phân vùng có thể dễ dàng được chuyển đổi giữa 2 chế độ mà không cần phải format như trước kia. Nhưng vấn đề vẫn còn tồn tại ở đây là những giới hạn của **Ext2** vẫn còn nguyên trong **Ext3**, và ưu điểm của **Ext3** là hoạt động nhanh, ổn định hơn rất nhiều. Không thực sự phù hợp để làm file hệ thống dành cho máy chủ bởi vì không hỗ trợ tính năng tạo **disk snapshot** và file được khôi phục sẽ rất khó để xóa bỏ sau này

**Ext4** cũng giống như **Ext3**, lưu giữ được những ưu điểm và tính tương thích ngược với phiên bản trước đó. Có thể dễ dàng kết hợp các phân vùng định dạng **Ext2**, **Ext3** và **Ext4** trong cùng 1 ổ đĩa trong **Ubuntu** để tăng hiệu suất hoạt động. Trên thực tế, **Ext4** có thể giảm bớt hiện tượng phân mảnh dữ liệu trong ổ cứng, hỗ trợ các file và phân vùng có dung lượng lớn... Thích hợp với ổ SSD so với **Ext3**, tốc độ hoạt động nhanh hơn so với 2 phiên bản **Ext** trước đó, cũng khá phù hợp để hoạt động trên server, nhưng lại không bằng **Ext3**.

**XFS** là một journaling filesystem 64 bit với hiệu năng cao. Có nhiều điểm tương đồng với Ext4: hạn chế được tình trạng phân mảnh dữ liệu, không cho phép các snapshot tự động kết hợp với nhau, hỗ trợ nhiều file dung lượng lớn, có thể thay đổi kích thước file dữ liệu… nhưng không thể shrink (chia nhỏ) phân vùng XFS. Một đặc tính quan trọng của XFS đó là khả năng bảo đảm tốc độ truy xuất dữ liệu cho các ứng dụng (Guaranteed Rate I/O), cho phép các ứng dụng duy trì được tốc độ truy xuất dữ liệu trên disk, rất quan trọng đối với các hệ thống phân phối dịch vụ video có độ phân giải cao hoặc các ứng dụng xử lý thông tin vệ tinh đòi hỏi duy trì ổn định tốc độ thao tác dữ liệu.

---

## 3. Đường dẫn

Đường dẫn là một phần quan trọng đối với người dùng khi mới bắt đầu học Linux, đây là thành phần sẽ xuyên suốt trong quá trình sử dụng các lệnh trên hệ thống

**Đường dẫn tuyệt đối** của một tệp tin hay thư mục luôn bắt đầu bởi **`/`** (root) và tiếp theo sau đó là chuỗi các thư mục mà nó đi xuyên qua cho đến khi tới đích. → Một đường dẫn tuyệt đối là đường dẫn bắt đầu bởi **`/`** (root)

**Đường dẫn tương đố**i không đòi hỏi phải bắt đầu từ **`/`** (root). Đường dẫn tương đối bắt đầu đi từ thư mục hiện tại. Một đường dẫn tương đối thường bắt đầu với tên của một thư mục hoặc tệp tin, kết hợp với các thư mục đặt biệt sau

- Dấu **`.`** (dấu chấm), thư mục **`.`** là thư mục đặc biệt, liên kết (biểu thị) đến thư mục hiện thời (working directory).
- Dấu **`..`** (hai chấm) liên kết (biểu thị) cho thư mục mẹ của thư mục hiện thời.

---

## 4. Các lệnh để di chuyển qua các thư mục (`cd` )

| Command | Description |
| --- | --- |
| cd | Chuyển về thư mục gốc /root  |
| cd [directory] | Chuyển đến thư mục yêu cầu  |
| cd .. | Chuyển về thư mục cha của thư mục hiện tại  |
| cd - | Chuyển về thư mục vừa rời đi Co |

---

## 5. Các option với lệnh `ls`

Xem các option của lệnh ls : man ls

| Command | Description |
| --- | --- |
| ls | Liệt kê các tệp tin tại thư mục hiện tại  |
| ls -a  | Liệt kê các tệp tin kể cả tệp tin ẩn bắt đầu bằng ‘.’ |
| ls - l | Hiển thị tệp hoặc thư mục, kích thước, ngày, thời gian đã sửa đổi, tên tệp hoặc tên thư mục và chủ sở hữu (owner) tệp file và đó là sự cho phép (permission). |

---

Nguồn tham khảo:

[Cấu trúc thư mục trong Linux](https://www.geeksforgeeks.org/linux-file-hierarchy-structure/)

[Cấu trúc thư mục trong Linux 2](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-the-linux-filesystem-explained)

[Giới thiệu một số file system phổ biến](https://blog.vinahost.vn/gioi-thieu-mot-so-file-system/)

---

Câu hỏi: 

- Phân biệt giữa /media và /mnt ?

[https://github.com/UocNTh/Learn-Linux/blob/main/Image/dev.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/dev.png?raw=true)
