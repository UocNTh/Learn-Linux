
# NFS - Thực hành

Nội dung tìm hiểu: 

- NFS là gì?
- Các phiên bản của NFS
- Cách thức hoạt động của NFS
- Ưu điểm, hạn chế của NFS
- Thực hành

**Bài toán:** 

Giả sử có một trang web bán hàng, ban đầu hệ thống có ít người dùng. Vậy nên thuê một server với 4GB RAM, CPU 2 Cores và ổ cứng 80GB SSD. Sau một thười gian thì server quá tải, bắt buộc để hệ thống hoạt động trơn tru thì phải thuê thêm một server nữa với thông số giống server 1. Trong quá trình deploy và chạy code trên môi trường production, thì phát hiện ra rằng mỗi lần gửi một request đến thư viện ảnh, thì response sẽ trả về những thông tin khác nhau (lúc có ảnh lúc không). Lý do là bức ảnh được yêu cầu nằm ở bên server 1 nên khi hệ thống Load Balance (Cân bằng tải), request sẽ được chuyển đến server 2 sẽ không lấy được ảnh vì ảnh nằm trên server 1, không nằm trên server 2. Vậy cần làm thế nào reponse trả về image? 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/nfs_04.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/nfs_04.png?raw=true)

**NFS là gì?** 

NFS (Network File System) là một hệ thống giao thức chia sẻ file, cho phép người dùng trên một máy tính khác truy cập tới hệ thống file chia sẻ thông qua một mạng máy tính giống như truy cập trực tiếp trên ổ cứng

**Những tính năng của NFS** 

- Cho phép truy cập cục bộ đến các tệp từ xa, cho phép nhiều máy tính sử dụng cùng một tệp để mọi người trên mạng có thể truy cập vào cùng một dữ liệu
- Có thể cấu hình các giải pháp tập trung (Cần tìm hiểu thêm)
- Giảm tri phí lưu trữ bằng cách các máy tính chia sẻ ứng dụng thay vì cần dung lượng ổ đĩa cục bộ cho mối ứng dụng riêng của người dùng

**Các hoạt động**

Để truy cập dữ liệu được lưu trữ trên 1 máy chủ, server sẽ triển khai các quy trình nền NFS để cung cấp dữ liệu cho khách hàng. Quản trị viên máy chủ xác định những gì cần cung cấp và đảm bảo có thể nhận ra các máy khác được xác nhận 

Từ client, yêu cầu quyền truy cập vào dữ liệu đã xuất, bằng cách sử dụng lệnh mount

Server NFS tham chiếu đến /etc/export để xác định xem máy khách có được cho phép truy cập vào bất kỳ hệ thống nào không. Sau khi xác minh, tất cả hoạt động tập tin và thư mục được phép sử dụng trên client

**Ưu điểm và nhược điểm**

**Ưu điểm:** 

- NFS là một giải pháp chi phí thấp để chia sẻ tệp mạng
- Dễ cài đặt vì sử dụng cơ sở hạ tầng IP hiện có
- Cho phép quản lý trung tâm và giảm nhu cầm thêm phần mềm cũ và dung lượng đĩa trên các hệ thống người dùng cá nhân

**Nhược điểm:** 

- Client và Server tin tưởng nhau vô điều kiện

**Giải bài toán**

Với bài toàn trên, đầu tiên thì cấu hình máy 1 NFS server để chia sẻ các tài nguyên (thư mục chứa ảnh), sau đấy coi các máy chủ còn lại là NFS client để có thể truy cập vào chia sẻ từ server 1. Quá trình này cho phép máy server 2 có thể truy cập đến thư mục ảnh có lấy được ảnh gửi về cho người dùng. Đặt vấn đề nếu ngược lại người dùng gửi một request yêu cầu một thông tin chứa trong server 2, thì tiếp tục thao tác các bước như trên, lúc này thì server 2 sẽ đóng vai trò là NFS server, và server 1 là NFS client. Tài nguyên chia sẻ lẫn nhau. Vậy nên lúc khi người dùng yêu cầu bất kỳ dữ liệu gì thì người dùng đều được trả lại dữ liệu đấy. 

### **Thực hành: Cài đặt và lưu trữ file theo mô hình : 1 máy cài NFS server, máy còn lại là NFS Client**

### **Tiến hành cài đặt máy Server:**

**Bước 1: Install NFS Server**

```bash
sudo apt-get update 
sudo apt-get install nfs-kernel-server
```

Khi thực hiện câu lệnh thì sẽ tạo thêm một file config /etc/exports. File này sẽ cho biết các client được quyền truy cập vào tài nguyên nào. 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/nfs_03.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/nfs_03.png?raw=true)

**Bước 2: Cấu hình máy chủ NFS trên Ubuntu 22.04**

- **Tạo một thư mục NFS dùng chung để chia sẻ tài nguyên**

```bash
mkdir -p /var/nfs/dir_share
```

Option -p: Nếu thư mục chưa có thì tạo mới, nếu có rồi thì không thực hiện tạo mới 

- Đặt **quyền truy cập thư mục**

```bash
sudo chown nobody:nogroup /var/nfs/dir_share
```

- **Cấp quyền truy cập NFS:** để cấp quyền truy cập cho client, cấu hình trong file **/etc/exports.**

```bash
sudo vim /etc/exports
```

Cú pháp: 

```bash
directory_to_share    client_ip(share_option1,...,share_optionN)
```

VD: 

```bash
# /etc/exports: the access control list for filesystems which may be exported
#               to NFS clients.  See exports(5).
#
# Example for NFSv2 and NFSv3:
# /srv/homes       hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_check)
#
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
# /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
#

/var/nfs/dir_share  192.168.24.0/22(rw,sync,no_subtree_check)
/home 192.168.24.0/22(rw,sync,no_root_squash,no_subtree_check)
```

Cấu hình này đang thiết lập dịch vụ NFS để chia sẻ thư mục "/var/nfs/dir_share" và “/home” với mạng con có các địa chỉ IP từ 192.168.24.0 đến 192.168.27.255.

**rw** - Tùy chọn cung cấp cho máy client có thể đọc và ghi 

**sync** - Buộc NFS ghi lại các thay đổi vào disk trước khi trả lời

**no_subtree_check -** Tùy chọn này ngăn việc kiểm tra subtree, đó là một tiến trình mà host phải kiểm tra xem liệu tệp đó có thực sự vẫn còn trong cây export cho mọi yêu cầu hay không. Điều này có thể gây ra nhiều vấn đề khi một tập tin được đổi tên trong khi client đã mở nó. Trong hầu hết các trường hợp, tốt hơn là để vô hiệu hóa việc kiểm tra subtree.

**no_root_squash** - Nếu từ client đăng nhập bằng tài khoản root, từ phía server sẽ chuyển vào non-privileged user trên server. Điều này vì lý do bảo mật.

- Restart dịch vụ

```bash
systemctl restart nfs-kernel-server
```

### Tiến hành cài đặt trên máy Client:

**Bước 1: Install** 

```bash
sudo apt-get update
sudo apt-get install nfs-common
```

**Bước 2: Cài đặt**

- **Tạo thư mục**

```bash
sudo mkdir -p /nfs/dir_share 
sudo mkdir -p /nfs/home
```

- **Mount thư mục cho Client**

```bash
sudo mount 192.168.25.225:/var/nfs/dir_share /nfs/dir_share
sudo mount 192.168.25.225:/home /nfs/home

```

- **Kiểm tra kết quả mount:** Sử dụng câu lệnh **df -h**

```bash
toe@UbuntuClient:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              197M  1.2M  196M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  8.1G  5.8G  1.9G  76% /
tmpfs                              983M     0  983M   0% /dev/shm
tmpfs                              5.0M     0  5.0M   0% /run/lock
/dev/sda2                          1.7G  253M  1.4G  16% /boot
tmpfs                              197M  4.0K  197M   1% /run/user/1000
192.168.25.225:/var/nfs/dir_share  8.1G  5.8G  1.9G  76% /nfs/dir_share
192.168.25.225:/home               8.1G  5.8G  1.9G  76% /nfs/home
```

### Kiểm tra

- Tạo file mới vào thư mục /nfs/dir_share bên phía Client
- Kiểm tra ownership của file vừa tạo

```bash
toe@UbuntuClient:/nfs/dir_share$ ls -l
total 0
-rw-r--r-- 1 nobody nogroup 0 Aug 10 12:10 hello_client.txt
-rw-r--r-- 1 root   root    0 Aug 10 12:11 hello_server.txt
-rw-r--r-- 1 nobody nogroup 0 Aug 10 15:37 test_client.txt
```

Các thay đổi từ phía client sẽ được thay đổi thành nobody nogroup 

- Kiểm tra bên phía server thư mục /var/nfs/dir_share

```bash
toe@UbuntuServer:/var/nfs/dir_share$ ls -l
total 0
-rw-r--r-- 1 nobody nogroup 0 Aug 10 12:10 hello_client.txt
-rw-r--r-- 1 root   root    0 Aug 10 12:11 hello_server.txt
-rw-r--r-- 1 nobody nogroup 0 Aug 10 15:37 test_client.txt
```

### **Mounting the Remote NFS Directories khi khởi động**

- Khi client tắt đi và khởi động lại, thì mount point đế Server sẽ bị mất đi. nếu muốn sử dụng phải tiến hành mount lại
- Để khắc phục vấn đề này, tiến hành cấu hình hệ thống mount tự động
- Chỉnh sửa file /etc/fstab

```bash
192.168.25.225:/var/nfs/dir_share    /nfs/dir_share   nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0
192.168.25.225:/home               /nfs/home      nfs auto,nofail,noatime,nolock,intr,tcp,actimeo=1800 0 0
```
