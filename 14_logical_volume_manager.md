# Disk và LVM

- Các loại storage
- Cấu tạo của hard disk ([Hard Disk Structure In OS » CS Taleem](https://cstaleem.com/hard-disk-structure-in-os) )
- Hiểu khái niệm LVM
- Thực hành thêm disk của VM và extend cho phân vùng / sử dụng LVM

---

### 1. Các loại storage

Có 3 loại storage: 

- Block Storage
- File Storage
- Object Storage

### 2. Cấu tạo của hard disk

### 3. Tìm hiểu về LVM

**3.1 Giới thiệu về LVM**

- Logical Volume Manager (LVM) là phương pháp cho phép ấn định không gian đĩa cứng thành những Logical Volume khiến cho việc thay đổi kích thước trở nên dễ dàng
- Một số những khái niệm:
    - **Physical Volume:** Ổ cứng vật lý từ hệ thống, là đơn vị cơ bản để LVM dùng để khởi tạo các Volume Group (VD: /dev/sda (Mặc định Linux đặt tên cho đĩa cứng thứ nhất)
    - **Volume Group**: Là tập hơn các ổ cứng vậy lý (PV) để thành một kho lữu trữ chung với tổng dung lượng là các ổ đĩa con. **Một điểm cần lưu ý: Boot Loader không thể đọc được /boot khi nó nằm trên Logical Volume Group. Do đó không thể sử dụng kỹ thuật LVM với /boot**
    
    ![https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-1.png](https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-1.png)
    
    - **Logical Volume**: là những phân vùng được tạo từ VG. Logical Volume tương tự các partition trên ổ cứng bình thường những linh hoạt hơn gì kích thước của LV có thể thay đổi dễ dàng theo thời gian thực mà không lo làm gián đoạn hệ thống
    
    ![https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-2.png](https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-2.png)
    
    - **extent**: là đơn vị nhỏ nhất của VG. Mỗi một volume được tạo ra từ VG chứa nhiều extent nhỏ với kích thước cố định bằng nhua. Các extent trên LV không nhất thiết phải nằm liên tục với nhau trên ổ cứng vật lý bên dưới mà có thể nằm rải rác trên nhiều ổ cứng khác nhau. Extent chính là nền tảng cho công nghệ LVM, các LV có thể mở rộng hay thu nhỏ bằng các thêm hoặc bớt đi các extent từ volume này.
    
    → Tóm lại, với công nghệ LVM thì người dùng có thể gộp nhiều ổ đĩa vật lý Physical Volume lại thành Volume Group để tổng hợp tài nguyên cần thiết. Sau đó, người quản trị có thể chia nhỏ các Volume Group ra thành các Logical Volume gồm nhiề extent, khi cần mở rộng Logical Volume thì người dùng thêm vào một số extent, khi cần thu nhỏ thì lấy một số extent. 
    
    ![https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-3.png](https://blog.vinahost.vn/wp-content/uploads/2020/12/gioi-thieu-va-huong-dan-mo-rong-LVM-3.png)
    

Tóm tắt hình: Người dùng có một VG được tạo ra từ 3 PV. Trên đó, ta tạo ra 3 LV và trong số đó có một LV chạy trên 2 PV khác nhau.

VD: Có 3 ổ đĩa cứng, mỗi ổ có 100GB, bạn có thể gộp được 3 PV thành 1 VG có 300GB, và bạn có thể tạo ra 1 LV 100GB hoặc 10 LV, trong đó mỗi LV có 10GB. 

### 4. Thực hành thêm disk của VM và extend cho phân vùng

**4.1 Chuẩn bị**

- Tạo máy ảo trên VitualBox cài hệ điều hành Ubuntu Server 22.04
- Thêm một số ổ cứng vào máy ảo

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/lvm-add-storage.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/lvm-add-storage.png?raw=true)

**4.2 Tạo Logical Volume trên LVM** 

**Bước 1: Kiểm tra các Hard Drives có trên hệ thống**

Có thể kiểm tra xem có những Hard Drives nào trên hệ thống bằng cách sử dụng câu lệnh **lsblk**

→ **lsblk**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_01.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_01.png?raw=true)

Trong đó có thể thấy sdb là Hard Drives vừa được thêm.

**Bước 2: Tạo partition**

Từ các Hard Drives trên hệ thống, chúng ta sẽ tiến hành tạo các partition. 

→ Tạo partition từ sdb sử dụng lệnh **fdisk /dev/sdb** 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_04.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_04.png?raw=true)

- Trong đó: ‘n’ là để bắt đầu tạo một partition
- Chọn ‘p’ là để tạp partition primary
- Chọn ‘1’ để tạo partition primary 1
- Tại First Sector để mặc định
- Tại Last Sector tạo ra partition có dung lượng 1G
- Chọn ‘w’ để lưu lại thay đổi

Tiếp theo thay đổi định dạng của partition vừa mới tạo thành LVM 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_05.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_05.png?raw=true)

- Chọn ‘t’ để thay đổi định dạng của partition. Nếu muốn hiển thị danh sách các định dạng, thì chọn L trong Hex code or alias. Để chuyển sang LVM thì chọn ‘8e’
- Có thể xem thông tin của partition bằng lệnh **fdisk -l /dev/sdc**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_06.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_06.png?raw=true)

**Bước 3: Tạo Physical Volume**

Để tạo ra các PV bằng lệnh sau: **pvcreate /dev/sdb2** 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_07.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_07.png?raw=true)

Có thể kiểm tra các PV bằng lệnh **pvs** hoặc có thể sử dụng lệnh ****pvdisplay****

**Bước 4: Tạo Volume Group** 

Sử dụng lệnh để tạo volume group: **vg vg1 /dev/sdb2 /dev/sdc1**

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_09.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_09.png?raw=true)

**Bước 5: Tạo Logical Volume**

Sử dụng câu lệnh: **lvcreate -L 1G -n lv1 vg1**

Các option: 

- -L: Chỉ ra dung lượng của logical volume
- -n: Tên của Logical Volume

**Bước 6: Định dạng Logical Volume** 

Để format các Logical Volume thành các định dạng như ext2, ext3, ext4, ta có thể làm như sau:

**mkfs -t ext4 /dev/vg1/lv1**

**Bước 7: Mount và sử dụng**

Tiến hành tạo thư mục và mount Logical Volume đã tạo vào thư mục đó 

Tạo thư mục: **mkdir demo** 

Mount logical volume vào thư mục demo: **mount /dev/vg1/lv1 demo** 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_11.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/08_08_11.png?raw=true)

Kiểm tra lại dung lượng của thư mục đã mount: **df -h** 

**4.3 Thay đổi dung lượng Logical Volume trên LVM**

Một số lệnh dùng để xem các thông tin hiện có:

**vgs**

**lvs**

**pvs**

Phần trước, mình đã tiến hành tạo một Logical Volume là vg1 và mình cấp cho lv1 là 1GB, giả sử dung lượng bị đầy và cần tăng kích thước của nó.

Do Logical Volume lv1 thuộc và Volume Group vg1, nên để tăng kích thước của lv1 trước hết phải xem vg1 còn dư dung lượng để bổ sung vào lv1 hay không. 

Kiểm tra Volume Group vg1 bằng lệnh vgdisplay

Để tăng kích thước của Logical Volume lv1, ta sẽ sử dụng câu lệnh: 

**lvextend -L +50M /dev/vg1/lv1** 

- -L: tăng kích thước

Sau khi tăng kích thước cho Logical Volume thì Logical Volume đã được tăng nhưng file system trên volume này vẫn chưa thay đổi, muốn vậy phải sửa dụng câu lệnh: **resize2fs /dev/vg1/lv1**
