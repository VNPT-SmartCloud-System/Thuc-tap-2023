# **VLAN**

![VLAN](img/VLAN(1).png)

## **1. VLAN là gì**

- **VLAN** là viết tắt của Virtual Local Network hoặc Virtual LAN có nghĩa là **Mạng cục bộ ảo** hoặc **Mạng LAN ảo**
- **VLAN** là một mạng tùy chỉnh được tạo từ một hay nhiều mạng LAN hiện có. Nó cho phép các nhóm thiết bị từ nhiều mạng (có dây và không dây) được kết hợp thành mạng logic duy nhất. Kết quả là một mạng LAN ảo có thể quản lý giống như một mạng cục bộ vật lý.
  
### **Cách hoạt động của VLAN**

- Các Virtual LAN ở trong mạng được xác định bằng một con số cụ thể
- Phạm vi giá trị hợp lệ là 1- 4094. Trên một switch VLAN, ta có thể chỉ định các cổng với số VLAN thích hợp
- Tiếp đến, switch sẽ cho phép dữ liệu cần được gửi giữa các port khác nhau có cùng một Virtual LAN.
- Vì hầu hết các mạng đều có nhiều hơn là chỉ một switch duy nhất. Vì vậy, cần có một cách nào đó để có thể gửi lưu lượng giữa hai switch trong mạng. Cách đơn giản nhất chính là gán một port trên mỗi switch của Virtual LAN và chạy một cable giữa chúng.

## **2. Ưu điểm và nhược điểm của VLAN**

![VLAN](img/VLAN(2).png)

**Ưu điểm**
- Giải quyết các vấn đề điển hình liên quan đến broadcast
- Giảm kích thước của broadcast domain
- Cho phép tạo thêm một lớp bảo mật bổ sung
- Giúp việc quản lý thiết bị trở nên đơn giản, dễ dàng hơn
- Cho phép tạo nhóm các thiết bị được kết nối hợp lý hoạt động giống như trên mạng riêng của chúng
- Cho phép phân đoạn mạng dựa trên các phòng ban, nhóm dự án hoặc chức năng
- Đem lại hiệu suất cao hơn, độ trễ (latency) thấp hơn
- Không cần thêm phần cứng, cáp, giúp tiết kiệm đáng kể chi phí

**Nhược điểm**
- Packet có thể bị rò rỉ giữa các VLAN
- Cần có một bộ định tuyến mạnh mẽ để kiểm soát một khối lượng công việc trong các mạng lớn.
- Một VLAN không thể chuyển tiếp lưu lượng mạng sang những VLAN khác

### **VLAN ranges**

Phạm vi|Miêu tả
---|---
VLAN 0 và 4095|VLAN dành riêng,không thể nhìn thấy hoặc sử dụng
VLAN 1|VLAN mặc định của switch. Không thể xóa,chỉnh sửa nhưng có thể được sử dụng
VLAN 2 – 1001|VLAN bình thường. Có thể tạo,sửa và xóa
VLAN 1002-1005|VLAN mặc đinh của Cisco cho vòng thông báo và FDDI. Không thể xóa VLAN này
VLAN 1006-4094|Nó là 1 phạm vi mở rộng của các VLAN

## **4. Trunking**

![VLAN](img/VLAN(3).png)

- Trong môi trường VLAN, một đường trunking là một kết nối point to point để hỗ trợ các switch kết nối với nhau.
- Một đường Trunking bao gồm nhiều lớp liên kết ảo trên một kết nối vật lý để truyền tín hiệu từ các VLAN trên các Switch với nhau trên một đường cap vật lý.
- Có 2 chuẩn của trunking:

**IEEE 802.1q**

![vlan4](img/VLAN(4).png)

- 802.1Q ko bao quanh frame bằng một header mới mà nó sẽ thêm trực tiếp 4bytes vào frame cũ. Như vậy, source add và dest add của frame được giữ nguyên ko bị thay đổi. Và bởi vì đã thêm 4bytes vào frame ban đầu nên sẽ phải tính toán lại FCS.
- Các trường trong 802.1Q VLAN Tag bao gồm:
    - Tag Protocol ID (16 bit) nôi dung trường này luôn được set 0x8100 dùng để định danh ra frame này đã được tag 802.1q để phân biệt với frame untagged trên đường trunk.
    - User Priority (3 bit) sử dụng cho kỹ thuật QoS.
    - Canonical Format Indicator (1bit) cho biết địa chỉ MAC đang được sử dụng ở định dạng Token Ring hay Ethernet Frame.
    - VLAN ID(12bit): cho biết Frame đang chạy trên đường trunk là của VLAN nào.

**ISL (chỉ dùng trong các thiết bị Cisco)**
    
![Vlan](img/VLAN(5).png)

ISL được Cisco tạo ra rất lâu trước khi IEEE định nghĩa giao thức trunking 802.1q. ISL là giao thức được tạo ra dành riêng cho các sw của Cisco hỗ trợ ISL bởi vì một số các sw mới của Cisco đã bỏ, ko hỗ trợ giao thức này.

Bằng cách thêm vào frame một ISL header có chứa VLAN ID, sw gửi sẽ chắc chắn rằng, sw nhận sẽ nhận được đúng frame mà nó cần nhận. ISL header sẽ sử dụng source và dest MAC add của sw chứ ko phải MAC của nơi gửi.

## **5. VLAN Trunking Protocol (VTP)**
### **5.1 Đặc điểm**

- Giúp cho việc cấu hình VLAN luôn đồng nhất khi thêm, xóa, sửa thông tin về VLAN trong hệ thống mạng.
- VTP hoạt động trên các đường Trunking Layer 2 để trao đổi thông tin VLAN với nhau
- 3 yếu tố quan trọng của VTP là : VTP domain, VTP password, VTP mode(Server, Client, Transparent). Trong đó VTP domain : các switch được tổ chức cùng thuộc một domain mới có thể chia sẻ thông tin VLAN với nhau.

### **5.2 VTP Mode**

![VTP](img/VTP(1).png)

- Server : switch hoạt động ở mode này có toàn quyền quyết định tạo, xóa, sửa thông tin VLAN. Đồng bộ thông tin VLAN từ các Switch khác, Forward thông tin VLAN đến các Switch khác.
- Client: switch hoạt động ở mode này không được thay đổi thông tin VLAN mà chỉ nhận thông tin VLAN từ Server. Đồng bộ thông tin VLAN từ switch khác và forward thông tin VLAN.
-  Transparent: switch hoạt động ở mode này không tiến hành tiếp nhận thông tin VLAN. Nó vẫn nhận được thông tin VLAN từ các Switch khác nhưng không tiến hành đồng bộ thông tin VLAN. Có thể tạo, xóa, sửa VLAN độc lập trên nó. Không gửi thông tin VLAN của bản thân cho các Switch khác nhưng nó có thể forward thông tin VLAN nhận được đến các Switch khác.

### **5.3 VTP Pruning**
 Tính năng hữu ích trong hoạt động trao đổi thông tin giữa các switch trong mạng chuyển mạch.
![VTP](img/VTP(2).png)

- Giả sử Host thuộc VLAN 10 tiến hành gửi một Frame đến Host khác cũng thuộc VLAN 10 nhưng nằm trong một Switch khác. Vì mỗi VLAN là một broadcast domain nên frame này sẻ được chuyển đến tất các các host thuộc VLAN 10 của Switch 2. Mặc định trên đường trunk sẽ cho qua dữ liệu của tất cả VLAN nên SW4 cũng nhận được frame này. Khi mà nó không tồn tại VLAN 10 nên việc forward frame đến SW4 gây lãng phí tài nguyên và băng thông hệ thống.
- Khi được bật tính năng VTP Prunning. SW4 sẻ gửi thông điệp báo cho SW1 rằng nó không cần dữ liệu của VLAN 10(vì không tồn  tại VLAN10). Và khi SW1 khi nhận được frame broadcast này sẻ tiến hành chặn frame này không forward nó qua đường trunk đến các SW không tồn tại VLAN 10(SW4).


## **Tài liệu tham khảo**
1. https://vietnix.vn/vlan/
2. https://wikimaytinh.com/vlan-la-gi-cau-hinh-vlan.html#VLAN_la_gi
3. https://ting3s.com/post/vlan-la-gi-cac-loai-vlan-uu-diem-va-nhuoc-diem-cua-vlan-845
4. https://itforvn.com/bai-6-vlan-trunking-vtp.html/