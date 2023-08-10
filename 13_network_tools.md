
# Network Tools

- ping (ý nghĩa các trường)
- traceroute (cách hoạt động)
- netstat (có những option nào)
- telnet, netcat

Mục tiêu: Hiểu được các giá trị trong output của các tool

---

### 1. Lệnh ping

ping là một trong những công cụ được sử dụng nhất để gỡ rối, kiểm tra và chuẩn đoán các vấn đề kết nối mạng 

- Output:

from: địa chỉ của máy IP mà máy nguồn ping tới  

tcmp_seq: là số thứ tự của gói ICMP được gửi đến và tăng 1 cho mỗi yêu cầu gửi tiếp theo 

ttl (time to live): giá trị mặc định trên Linux là 64, khi đi qua mỗi router thì giá trị ttl sẽ giảm đi 1, vì vậy có thể tham số này chúng ta có thể đoán được là gói tin đã đi qua bao nhiêu trạm trước khi đến đích

time: dựa vào thời gian trả về trong lệnh ping chúng ta sẽ đoán được độ ổn định của mạng, các giá trị time trả về càng ngắn thì độ ổn định càng cao

Trường hợp thất bại: (có thể suy ra được một số vấn đề)

- Mạng gặp vấn đề
- Nghẽn mạng
- Tường lửa của máy đích chặn

Một số lỗi trả về khi dùng lệnh ping: 

- **Destination Host Unreachable**: không có đường đi tới địa chỉ đích hoặc sai địa chỉ đích, khi lệnh ping gặp lỗi này nó sẽ trả về kèm theo IP của nơi cuối cùng mà gói tin đi được tới.
- **Request time out**: Lỗi này xuất hiện khi không kết nối được đến máy đích và không có đáp hồi trả về. Nguyên nhân của lỗi này là do các thiết bị định tuyến router bị tắt hoặc địa chỉ máy đích không có thật, bị tắt hay cấm ping.
- **TTL expired in transit**: Lỗi này xuất hiện khi giá trị TTL (Time To Live) được đặt cho gói ping giảm xuống 0 trong khi di chuyển qua mạng trước khi đến đích.

---

### 2. Lệnh traceroute

Là công cụ để chuẩn đoán mạng máy tính để hiển thị các tuyến đường và đo lường sự chậm trễ quá cảnh của các gói tin dữ liệu trên giao thức IP 

**traceroute hoạt động như thế nào?**

- Khi bạn truy cập vào một website nào đó, các lưu lượng truy vấn sẽ phải đi quan nhiều trạm trung gian trước khi đi được đến website bạn yêu cầu, những lưu lượng này sẽ đi từ máy tính của bạn đến các route của nhà cung cấp dịch vị (ISP) và được chuyển tiếp đến nhiều các route trung gian khác trên mạng trước khi đến được website
- Traceroute hoặc động bằng các gửi đi một chuỗi các gói tin bằng giao thức ICMP tới máy chủ đích, các gói tin này chứa một giá trị ttl (time to live) hay còn gọi là Hop Limit, giá trị của các gói tin được săp xếp theo thứ tự tăng dần, gói thứ nhất chứa giá trị ttl là 1, gói thứ 2 chứa giá trị ttl là 2. Khi các gói tin đến một router, giá trị của nó giảm đi 1 cho đến khi giá trị ttl của các gói tin là 0, router sẽ gửi một thông báo hết hạn cho máy tính của bạn. Bằng việc gửi đi các tin và xem phản hồi của các router, traceroute sẽ xác định được một router nào đó có hoạt động tốt không

---

### 3. Lệnh netstat

Là công cụ theo dõi các thông số về mạng

Một số option được sử dụng 

| Option | Description  |
| --- | --- |
| -a | Liệt kê tất cả các socket (đang lắng nghe và không lắng nghe) |
| -l  | Hiển thị các socket đang lắng nghe  |
| -t | Hiển thị các kết nối tcp |
| -u  | Hiển thị các kết nối udp |
| -r  | Hiển thị bảng định tuyến  |

### 4. Telnet

Là giao thức hỗ trợ kết nối Internet và hệ thống mạng cục bố LAN. Được xem như nền tảng của giao thức SSH 

![https://fptcloud.com/wp-content/uploads/2022/03/Telnet-giao-thuc-ho-tro-ket-noi-internet-va-he-thong-mang-cuc-bo-LAN.jpg](https://fptcloud.com/wp-content/uploads/2022/03/Telnet-giao-thuc-ho-tro-ket-noi-internet-va-he-thong-mang-cuc-bo-LAN.jpg)

**Khác biệt giữa Telnet và SSH?**

- Sự khác biệt nữa Telnet và SSH là tính bảo mật. Telnet khi gửi dữ liệu sẽ gửi qua text là không qua bất kỳ các cơ chế mã hóa. Dẫn đến các dữ liệu được truyền bằng telnet có thể bị tấn công. SSH sử dụng mã khóa để xác thực nne thông tin được gửi bằng SSH sẽ an toàn hơn. (Telnet dùng mã hóa công khai để xác thực người dùng từ xa)

Hiện tại thì cái này không hay được sử dụng với chức năng truy cấp máy chủ từ xa do tích bảo mật của nó không tốt. Mục đích hiện tại người ta sử dụng là để kiểm tra xem cái network có thông hay không. 

Các sử dụng: VD telnet [google.com](http://google.com) 443 

Gửi được gói tin hiện tại có đến được gói đích hay không 

![https://github.com/UocNTh/Learn-Linux/blob/main/Image/web.png?raw=true](https://github.com/UocNTh/Learn-Linux/blob/main/Image/web.png?raw=true)

Giải thích hình: Giả sử đường truyền không thông, muốn kiểm tra thì có thể đứng ở vị trí Nginx để kiểm tra App có đang hoạt động được hay không (có thể do network chặn) nên để kiểm tra thì mình sẽ đứng Nginx và telnet kiểm tra xem có thông được với APP hay không, tương tự với kiểm tra. 

## Netcat

Được sử dựng để kiểm tra tương tự telnet.

**nc -zv [google.com](http://google.com/) 443**

---

**ICMP Echo** 

- **ICMP Echo** còn được gọi là ICMP Echo Request và ICMP Echo Reply, là một loại thông báo kiểm soát mạng được sử dụng trong giao thức IP. Nó thường được sử dụng để kiểm tra tính hoạt động và sẵn sàng cho một thiết bị mạng, chẳng hạn như máy tính hoặc một thiết bị mạng khác, thông qua việc gửi yêu cầu và chời đợi phản hồi.
- Trong giao thức ICMP, một thiết bị gửi một thông điêp ICMP Echo Request (yêu cầu ping) đến một địa chỉ IP cụ thể. Thiết bị mục tiêu sau đó sẽ gửi một phản hồi bằng cách gửi một thông điệp “ICMP Echo Reply” (phản hồi ping) để cho biết rằng nó vẫn hoạt động và giao tiếp.
- Chức năng này thường được sử dụng để kiểm tra kết nối và đo thười gian phản hồi của một máy tính hoặc thiết bị trong mạng.

---

**Giá trị TTL trong ping và giá trị TTL trong traceroute là khác nhau?**

- **TTL trong lệnh ping:** Trong lệnh ping, giá trị TTL được sử dụng để xác định số lượng bước trung gian (router) mà gói tin sẽ đi qua trước khi bị hủy. Khi gửi một gới tin ICMP Echo Request, giá trị TTL ban đầu thường là 64 (Linux). Mỗi gói tin khi đi qua một router, giá tị TTL sẽ giảm đi 1. Nếu giá trị TTL thành 0, router đó sẽ hủy gói tin và gửi một thông báo ICMP cho máy gửi để thông báo gói tin đã bị huy do vươt quá số lần cho phép
- **TTL trong lệnh traceroute:** Trong lệnh traceroute, giá trị TTL được sử dụng để xác định số lượng bước trung gian mà gói tin sẽ đi qua trước khi bị hủy. Giá trị TTL sẽ được thay đổi tăng dần cho mỗi gói tin (bắt đầu từ 1). Khi một gói tin đi qua một router, giá trị TTL sẽ giảm đi 1.
