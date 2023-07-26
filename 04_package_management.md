# Package Management

Nội dung: 

- Cách hoạt động của Package system
- Các hoạt động chính ( Tìm kiếm, install, remove, ….)
- Phân biệt apt , yum

---

Các bản phân phối khác nhau sẽ sử dụng hệ thống đóng gói khác nhau và theo một nguyên tắc chung, một gói dành cho bản phân phối này sẽ không tương thích với bản phân phối khác. 

Hầu hết các bản phân phối chia thành 2 loại: Debian Style và Red Hat Style

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/package-management.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/package-management.png?raw=true)

---

## 1. Cách hoạt động của Package System

**Package Files:** là một file compressed chứa tất cả các thông tin cần thiết để cài đặt phần mềm. Được tạo bởi package maintainer.

**Repositories**: Nơi chứa các package files. Một bản phân phối có thể có một vài kho lưu trữ khác nhau cho các giai đoạn khác nhau của vòng đời phát triển phần mềm. 

**Dependencies:** Một chương trình ít khi “standalone” mà thường có được xây dựng dựa trên các thành phần của một phần mềm khác. Hệ thống quản lý các package sẽ cung cấp các phương thức để khi cài đặt package thì tất cả các dependencies của package sẽ được cài đặt.

Package management systems được chia làm hai loại công cụ:

- Low-level tools: Dùng để thực hiện các tác vụ như: install và remove
- High-level tools: Dùng để xử lý các tác vụ liên quan đến tìm kiếm thông tin metadata và cài đặt dependencies

| Distributions | Low-level tools | High-level tools |
| --- | --- | --- |
| Debian-Style | dpkg (debian package) | apt-get, apt |
| Red Hat Style | rpm | yum |

---

## 2. Các hoạt động chính

******Tìm kiếm package trên repository******

- Sử dụng high-level tools: Có thể tìm kiếm theo tên hoặc theo mô tả
- Câu lệnh: apt-cache search search_string

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/find_package.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/find_package.png?raw=true)

VD Tìm kiếm apache

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/example%20apt-cache%20search%20.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/example%20apt-cache%20search%20.png?raw=true)

**Cài đặt package từ repository**

- Sử dụng high-level tools để tải gói từ kho lưu trữ và cài đặt cùng với các dependency cần thiết cho chương trình
- Câu lệnh: apt-get install package_name

**Cài đặt package từ package file**

- Được sử dụng để cài đặt package từ package file đã được download về máy, tuy nhiên lệnh low-level sẽ không có dependency resolution nên sẽ không tự động cài đặt được các dependency cần thiết
- Câu lệnh: dpkg -i package_file

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/install%20dpkg.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/install%20dpkg.png?raw=true)

**Xóa package**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/remove%20package.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/remove%20package.png?raw=true)

**Cập nhật package từ respository**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/update%20package%20high-tools.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/update%20package%20high-tools.png?raw=true)

**Cập nhật package từ package file**

- Đối với những package đã download sẵn file package chứa version mới nhất về máy, ta có thể chạy lệnh low-level sau để update

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/update%20package%20dpkg.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/update%20package%20dpkg.png?raw=true)

**Hiện danh sách các package đã được cài đặt**

- Câu lệnh: dpkg -l

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/show%20list%20.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/show%20list%20.png?raw=true)

VD Giả sử khi install nginx thì có thể sử dụng câu lệnh: dpkg -l | grep nginx để dễ dàng tìm kiếm hơn.

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/nginx%20.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/nginx%20.png?raw=true)

**Xác định khi một package đã được cài đặt:**

- Câu lệnh: dpkg -s package_name

**Hiển thị thông tin về gói đã cài đặt**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/info%20package%20installed.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/info%20package%20installed.png?raw=true)

**Tìm package nào đã cài đăt file** 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/find%20package%20install%20a%20file%20.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/find%20package%20install%20a%20file%20.png?raw=true)

---

| Mô tả | Câu lệnh |
| --- | --- |
| Tìm kiếm package trên repository | apt-cache search string_search |
| Cài đặt package từ repository | apt-get install package_name |
| Cài đặt package từ package file | dpkg -i package_file |
| Xóa package  | apt-get remove package_name |
| Cập nhật package từ repository | apt-get update; apt-get upgrade |
| Cập nhật package từ package files | dpkg -i package_file |
| Hiển thị danh sách package  | dpkg -l  |
| Xác định package đã được cài đặt hay chưa  | dpkg -s package_name |
| Hiển thị thông tin của một package  | apt-cache show package_name  |
| Tìm package nào đã cài đặt file | dpkg  —search file_name |

## 3. Phân biệt apt và yum

**APT (Advanced Package Tool)**:

- **`apt`** là công cụ quản lý gói phần mềm chủ yếu được sử dụng trên các hệ điều hành dựa trên Debian như Ubuntu, Debian và các bản phân phối khác. Nó được thiết kế để giúp người dùng cài đặt, cập nhật và gỡ bỏ các phần mềm dễ dàng từ các kho lưu trữ (repositories) của hệ điều hành.
1. **YUM (Yellowdog Updater Modified)**:
    - **`yum`** là công cụ quản lý gói phần mềm được sử dụng chủ yếu trên các hệ điều hành dựa trên Red Hat như CentOS, Fedora và các bản phân phối khác. Giống như APT, **`yum`** cung cấp khả năng cài đặt, cập nhật và gỡ bỏ phần mềm từ các kho lưu trữ của hệ điều hành.
    

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/package-management.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/package-management.png?raw=true)

---

Câu hỏi: 

**? Trong thư mục /etc/apt có file sources.list, file này là gì?** 

Trong các kho lưu trữ dùng để cung cấp các gói cho người dùng. Ubuntu và các bản phân phối dựa trên Debian sẽ sử dụng file **sources.list** để lưu giữ bản ghi của tất cả các kho lưu trữ trên hệ thống.

Ex: 

```bash
root@ToeUbuntu:/etc/apt# cat sources.list
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://vn.archive.ubuntu.com/ubuntu jammy main restricted
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://vn.archive.ubuntu.com/ubuntu jammy-updates main restricted
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://vn.archive.ubuntu.com/ubuntu jammy universe
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy universe
deb http://vn.archive.ubuntu.com/ubuntu jammy-updates universe
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team, and may not be under a free licence. Please satisfy yourself as to
## your rights to use the software. Also, please note that software in
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://vn.archive.ubuntu.com/ubuntu jammy multiverse
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy multiverse
deb http://vn.archive.ubuntu.com/ubuntu jammy-updates multiverse
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-updates multiverse

## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
deb http://vn.archive.ubuntu.com/ubuntu jammy-backports main restricted universe multiverse
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-backports main restricted universe multiverse

deb http://vn.archive.ubuntu.com/ubuntu jammy-security main restricted
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-security main restricted
deb http://vn.archive.ubuntu.com/ubuntu jammy-security universe
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-security universe
deb http://vn.archive.ubuntu.com/ubuntu jammy-security multiverse
# deb-src http://vn.archive.ubuntu.com/ubuntu jammy-security multiverse
```

**? Lệnh apt-get update và lệnh apt-get upgrade có chức năng gì?**

**Lệnh apt-get update:** 

- Kết nối với các kho lưu trữ đã được cấu hình trong file sources.list hoặc thực mục sources.list.d
- Lệnh này được sử dụng để tải thông tin package từ tất cả các kho lưu trữ đã được cấu hình. Đưa ra thông tin về phiên bản cập nhật của các gói và các dependency

**Lệnh apt-get upgrade:**

- Để cài đặt các bản nâng cấp có sẵn của các gói được cài đặt trên hệ thống từ các nguồn được cấu hình