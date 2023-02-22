

# ***VLAN là gì***
- VLAN là viết tắt của Virtual Local Area Network, là một công nghệ mạng được sử dụng để phân chia một mạng vật lý thành nhiều mạng ảo độc lập với nhau trên cùng một thiết bị chuyển mạch (switch).

Với VLAN, các thiết bị trên mạng vật lý được chia thành các nhóm khác nhau, có thể là theo địa chỉ IP, theo tên miền, theo chức năng hoặc theo bất kỳ tiêu chí nào khác. Các thiết bị trong cùng một VLAN có thể giao tiếp với nhau nhưng không thể truy cập vào các thiết bị của các VLAN khác. Điều này cung cấp tính bảo mật cho mạng và giúp giảm tải cho các thiết bị mạng.
- ![ima](./ImaVlan/1.png)
- Nếu không có mạng Virtual LAN, một broadcast được gửi từ host có thể dễ dàng đi đến mọi thiết bị mạng. Khi đó, tất cả thiết bị đều sẽ xử lý những frame đã nhận broadcast đó. Việc này sẽ làm tăng đáng kể chi phí cho CPU trên mỗi thiết bị, đồng thời làm giảm khả năng bảo mật của hệ thống.

- Nếu ta đặt các interface trên các switch ở những VLAN riêng biệt, một broadcast từ host A chỉ có thể đi đến các thiết bị khả dụng ở trong cùng một Virtual LAN. Các host của Virtual LAN sẽ không hề biết về cách thức giao tiếp.

# ***Phân loại Vlan***
## ***Static Vlan(Vlan tĩnh)
- Static VLAN là loại VLAN được tạo ra bằng cách gắn các cổng Switch vào một VLAN. Cách làm này tương tự như việc một thiết bị được kết nối vào mạng và nó tự mình công nhận bản thân là VLAN của cổng đó.

- Trong trường hợp người dùng cần thay đổi các cổng và có nhu cầu truy cập vào một VLAN chung, quản trị viên phải khai báo cổng cho VLAN trong lần kết nối tiếp theo.

## ***Dynamic Vlan(Vlan động)

- Được biết Dynamic VLAN là loại VLAN được tạo ra bằng cách sử dụng những phần mềm điển hình như Ciscowork 2000. Khi này người dùng sẽ sử dụng VLAN Management Policy Server (VMPS) để đăng ký các cổng Switch kết nối tới VLAN tự động. Quá trình kết nối được thực hiện dựa trên địa chỉ MAC nguồn của loại thiết bị được kết nối tới cổng.

- Tương tự như mô hình thiết bị mạng, Dynamic VLAN hoạt động truy vấn một cơ sở dữ liệu dựa trên VMPS của các VLAN thành viên còn lại.
# ***Cách hoạt động của VLAN***
- Các Virtual LAN ở trong mạng được xác định bằng một con số cụ thể
- Phạm vi giá trị hợp lệ là 1- 4094. Trên một switch VLAN, ta có thể chỉ định các cổng với số VLAN thích hợp.
- Tiếp đến, switch sẽ cho phép dữ liệu cần được gửi giữa các port khác nhau có cùng một Virtual LAN.
- Vì hầu hết các mạng đều có nhiều hơn là chỉ một switch duy nhất. Vì vậy, cần có một cách nào đó để có thể gửi lưu lượng giữa hai switch trong mạng. Cách đơn giản nhất chính là gán một port trên mỗi switch của Virtual LAN và chạy một cable giữa chúng.
# ***Ưu điểm của Vlan***
- Giảm tải mạng: Khi một địa chỉ broadcast được gửi trên mạng vật lý, nó sẽ ảnh hưởng đến tất cả các thiết bị trên mạng. Khi chia mạng vật lý thành các VLAN, các địa chỉ broadcast chỉ được gửi đến các thiết bị trong cùng VLAN, giảm tải cho các thiết bị không cần nhận địa chỉ broadcast.

- Tăng tính bảo mật: Với VLAN, các thiết bị trong cùng VLAN có thể giao tiếp với nhau nhưng không thể truy cập vào các thiết bị của các VLAN khác. Điều này giúp giảm khả năng bị tấn công mạng.

- Dễ dàng quản lý: Với VLAN, các thiết bị trên mạng vật lý có thể được chia thành các nhóm khác nhau, tùy thuộc vào các tiêu chí cụ thể. Điều này giúp cho việc quản lý mạng dễ dàng hơn.
# ***Nhược điểm của Vlan***
- Packet có thể bị rò rỉ giữa các VLAN
- Packet được inject có thể dẫn đến cyber attack
- Các mối đe dọa ở trong một hệ thống đơn lẻ có thể phát tán virus cho toàn bộ mạng
- Cần có một router bổ sung để kiểm soát workload trong những mạng lớn
- Khả năng tương tác có thể gặp vấn đề
Một VLAN không thể chuyển tiếp lưu lượng mạng sang những VLAN khác
# ***Ứng dụng Vlan***
- Tăng tính bảo mật: VLAN giúp tăng tính bảo mật cho mạng bằng cách phân chia mạng vật lý thành nhiều mạng ảo độc lập với nhau. Việc phân chia này giúp ngăn chặn các cuộc tấn công từ các thiết bị không được phép trong cùng một VLAN và giảm thiểu sự lan truyền của các thông tin bảo mật trên toàn mạng.

- Quản lý dễ dàng: VLAN giúp quản lý mạng dễ dàng hơn bằng cách phân chia mạng vật lý thành các mạng ảo độc lập với nhau tùy thuộc vào các tiêu chí nhất định. Việc này giúp cho việc quản lý mạng trở nên dễ dàng hơn.

- Giảm tải mạng: VLAN giúp giảm tải mạng bằng cách giảm lượng thông tin broadcast và multicast trên mạng. Khi một địa chỉ broadcast được gửi trên mạng vật lý, nó sẽ ảnh hưởng đến tất cả các thiết bị trên mạng. Khi chia mạng vật lý thành các VLAN, các địa chỉ broadcast chỉ được gửi đến các thiết bị trong cùng VLAN, giảm tải cho các thiết bị không cần nhận địa chỉ broadcast.

- Tăng cường hiệu suất: VLAN giúp tăng cường hiệu suất mạng bằng cách tối ưu hóa lưu lượng truyền thông giữa các thiết bị trong cùng VLAN. Việc tối ưu hóa này giúp giảm thời gian chờ đợi trong việc truyền thông giữa các thiết bị và tăng tốc độ truyền thông trên mạng.

- Phân tích lưu lượng mạng: VLAN giúp phân tích và quản lý lưu lượng truyền thông trên mạng. Việc này giúp người quản trị mạng có thể quản lý và giám sát lưu lượng mạng một cách hiệu quả hơn.
![ima](./ImaVlan/2.png)

# ***Tìm hiểu VTP***
## ***Khái niệm***   
   - Giao thức đồng bộ thông tin VLAN giữa các thiết bị Switch. Khi một hệ thống lớn thì việc tạo, xóa, sửa VLAN trong các Switch trở nên cực kì khó khăn. Thiếu tính chính xác và mất nhiều thời gian.Giao thức VTP tiến hành đồng bộ thông tin và cấu hình VLAN giữa các Switch trong cùng một miền Domain.
![ima](./ImaVlan/3.png)


## ***Một số lợi ích của VTP bao gồm:***

- Tiết kiệm thời gian và công sức của quản trị viên mạng khi cấu hình VLAN trên các thiết bị mạng.
- Đảm bảo tính nhất quán và đồng bộ hóa thông tin VLAN trên toàn bộ mạng.
## ***Tuy nhiên, VTP cũng có một số hạn chế và rủi ro, bao gồm:***

- Khả năng gây ra sự cố nếu thiết bị VTP Server bị lỗi và phát tán thông tin sai về các VLAN trên mạng.
- Không phù hợp cho các mô hình mạng phức tạp với nhiều VTP Domain.
- Không bảo mật trong việc phân phối thông tin VLAN, do đó cần thực hiện các biện pháp bảo mật bổ sung để đảm bảo tính an toàn và bảo mật của mạng.

# ***Tìm hiểu STP***
## ***Khái niệm***
STP là viết tắt của "Spanning Tree Protocol". Đây là một giao thức mạng được sử dụng để đảm bảo tính tin cậy và tránh các vòng lặp trên mạng Ethernet. Khi một mạng Ethernet có nhiều đường kết nối, STP sẽ tính toán và chọn ra một đường kết nối duy nhất để truyền dữ liệu giữa các thiết bị, đồng thời ngăn chặn các vòng lặp trên mạng.

Khi được kích hoạt, STP sẽ xác định các đường kết nối trên mạng và xây dựng một cây cầu ảo (Virtual Bridge Network) bằng cách chọn ra một đường kết nối chính và các đường kết nối dự phòng để tránh các vòng lặp trên mạng. Các đường kết nối dự phòng sẽ được giữ trong trạng thái chờ đợi, sẵn sàng chuyển đổi vào khi đường kết nối chính gặp sự cố.

![ima](./ImaVlan/4.png)
## ***Một số lợi ích của STP bao gồm:***

Đảm bảo tính tin cậy và ổn định của mạng Ethernet.
Ngăn chặn các vòng lặp trên mạng Ethernet.
Cho phép tối đa hóa băng thông sử dụng bằng cách sử dụng nhiều đường kết nối trên mạng.
## ***Tuy nhiên, STP cũng có một số hạn chế và rủi ro, bao gồm:***

Tốc độ hội tụ chậm khi đường kết nối chính gặp sự cố và phải chuyển đổi sang đường kết nối dự phòng.
Mất băng thông khi các đường kết nối dự phòng không được sử dụng.
Không bảo mật trong việc phát hiện và chọn ra đường kết nối chính trên mạng Ethernet, do đó cần thực hiện các biện pháp bảo mật bổ sung để đảm bảo tính an toàn và bảo mật của mạng.

# ***Tài liệu tham khảo***
<https://vietnix.vn/vlan/#:~:text=VLAN%20%28Virtual%20Local%20Area%20Network%29%20l%C3%A0%20m%E1%BB%99t%20m%E1%BA%A1ng,l%C3%BD%20gi%E1%BB%91ng%20nh%C6%B0%20m%E1%BB%99t%20m%E1%BA%A1ng%20LAN%20v%E1%BA%ADt%20l%C3%BD.>

<https://itforvn.com/bai-6-vlan-trunking-vtp.html/>

<https://itforvn.com/tu-hoc-ccnax-bai-7-spanning-tree.html/>
<https://trogiupnhanh.com/vtp-la-gi-cong-dung-cua-vtp/>
<https://thegioimang.vn/dien-dan/threads/t%C3%ACm-hi%E1%BB%83u-giao-th%E1%BB%A9c-stp-spanning-tree-protocol-c%E1%BA%A5u-h%C3%ACnh-stp-tr%C3%AAn-switch-cisco.588/>