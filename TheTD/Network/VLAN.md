# **VLAN**

![VLAN](img/VLAN(1).png)

## **1. VLAN là gì**

**VLAN (Virtual Local Area Network)** là một công nghệ trong mạng máy tính cho phép chia một mạng vật lý thành nhiều mạng logic (virtual network) độc lập nhau, giúp kiểm soát và quản lý truy cập tài nguyên mạng hiệu quả hơn. VLAN cho phép chia mạng theo địa chỉ IP, cổng Switch, giao thức và các tiêu chí khác.

Trong một mạng vật lý thông thường, các thiết bị mạng được kết nối với nhau thông qua một switch hoặc hub. Các thiết bị này được phân bố trong cùng một mạng và có thể truy cập vào tất cả các tài nguyên mạng. Tuy nhiên, với VLAN, các thiết bị được phân chia thành nhiều mạng logic khác nhau, mỗi mạng độc lập với nhau và có thể được kiểm soát truy cập.

Ví dụ, trong một doanh nghiệp, chúng ta có thể phân chia mạng thành các VLAN khác nhau tùy theo phòng ban, ví dụ: VLAN cho phòng kế toán, VLAN cho phòng nhân sự, VLAN cho phòng kinh doanh... Điều này giúp đảm bảo an toàn thông tin, chia sẻ tài nguyên và quản lý truy cập mạng.

Mỗi VLAN được xác định bằng một định danh duy nhất, được gọi là VLAN ID (VD: 10, 20, 30,...). Các thiết bị trong cùng một VLAN có thể giao tiếp với nhau nhưng không thể truy cập vào các thiết bị ở các VLAN khác, trừ khi được cấu hình đặc biệt. Trong cùng một switch, chúng ta có thể có nhiều VLAN khác nhau, các VLAN này không giao tiếp với nhau, chỉ giao tiếp qua các thiết bị định tuyến (router).

Nếu không có mạng Virtual LAN, một broadcast được gửi từ host có thể dễ dàng đi đến mọi thiết bị mạng. Khi đó, tất cả thiết bị đều sẽ xử lý những frame đã nhận broadcast đó. Việc này sẽ làm tăng đáng kể chi phí cho CPU trên mỗi thiết bị, đồng thời làm giảm khả năng bảo mật của hệ thống.

Nếu ta đặt các interface trên các switch ở những VLAN riêng biệt, một broadcast từ host A chỉ có thể đi đến các thiết bị khả dụng ở trong cùng một Virtual LAN. Các host của Virtual LAN sẽ không hề biết về cách thức giao tiếp.

Để triển khai VLAN, chúng ta cần phải có switch có khả năng hỗ trợ VLAN (VLAN-enabled switch). Các thiết bị trong mạng cũng cần phải được cấu hình để hoạt động trong các VLAN tương ứng. Một số switch có thể được cấu hình bằng cách sử dụng VLAN trực quan (VLAN GUI) để giúp người dùng dễ dàng cấu hình VLAN.

## **2. Cách hoạt động của VLAN**

- Các Virtual LAN ở trong mạng được xác định bằng một con số cụ thể
- Phạm vi giá trị hợp lệ là 1- 4094. Trên một switch VLAN, ta có thể chỉ định các cổng với số VLAN thích hợp
- Tiếp đến, switch sẽ cho phép dữ liệu cần được gửi giữa các port khác nhau có cùng một Virtual LAN.
- Vì hầu hết các mạng đều có nhiều hơn là chỉ một switch duy nhất. Vì vậy, cần có một cách nào đó để có thể gửi lưu lượng giữa hai switch trong mạng. Cách đơn giản nhất chính là gán một port trên mỗi switch của Virtual LAN và chạy một cable giữa chúng.

## **3. Ưu điểm và nhược điểm của VLAN**

![VLAN](img/VLAN(2).png)

**Ưu điểm**
- Giải quyết các vấn đề điển hình liên quan đến broadcast
- Giảm kích thước của broadcast domain
- Cho phép tạo thêm một lớp bảo mật bổ sung
- Giúp việc quản lý thiết bị trở nên đơn giản, dễ dàng hơn
- Cho phép tạo một nhóm logic các thiết bị, phân loại theo chức năng
- Có thể tạo các nhóm thiết bị được kết nối logic, có thể hoạt động như trên mạng riêng của mình
- Cho phép phân đoạn mạng dựa trên nhóm, hay chức năng
- Có thể cấu trúc mạng theo vị trí địa lý
- Đem lại hiệu suất cao hơn, độ trễ (latency) thấp hơn
- Người dùng có thể bảo vệ những thông tin nhạy cảm của mình
- Xóa bỏ ranh giới vật lý
- Tăng cường bảo mật mạng
- Không cần thêm phần cứng, cáp, giúp tiết kiệm đáng kể chi phí
- Việc thay đổi IP subnet của người dùng sẽ nằm trong phần mềm
- Giảm số lượng thiết bị cho cấu trúc liên kết mạng
- Đơn giản hóa việc quản lý các thiết bị vật lý

**Nhược điểm**
- Packet có thể bị rò rỉ giữa các VLAN
- Các mối đe dọa ở trong một hệ thống đơn lẻ có thể phát tán virus cho toàn bộ mạng
- Cần có một router bổ sung để kiểm soát workload trong những mạng lớn
- Khả năng tương tác có thể gặp vấn đề
- Một VLAN không thể chuyển tiếp lưu lượng mạng sang những VLAN khác

## **4. Ứng dụng của VLAN**

![VLAN](img/VLAN(3).png)

Các ứng dụng của VLAN bao gồm:

- Tăng tính an toàn mạng: Một phần của mạng VLAN có thể được cấu hình để không có quyền truy cập từ bên ngoài, chỉ cho phép các thiết bị trong phần đó có thể truy cập vào nhau. Điều này giúp ngăn chặn các cuộc tấn công mạng từ bên ngoài.

- Tăng tính linh hoạt: Quản trị viên mạng có thể tùy chỉnh các phần của mạng VLAN để phù hợp với yêu cầu sử dụng cụ thể của tổ chức. Điều này cho phép mạng được tối ưu hóa và dễ dàng mở rộng khi cần thiết.

- Giảm chi phí: Việc sử dụng VLAN có thể giúp giảm chi phí cho tổ chức bằng cách giảm số lượng thiết bị mạng cần thiết. Với VLAN, một switch có thể được sử dụng để phân chia mạng thành nhiều phần, thay vì phải sử dụng nhiều switch.

- Tăng tính đồng nhất: Các phần của mạng VLAN có thể được cấu hình giống nhau, giúp tăng tính đồng nhất của mạng. Điều này giúp quản trị viên mạng dễ dàng quản lý toàn bộ mạng nội bộ.

- Tăng hiệu suất mạng: Một phần của mạng VLAN có thể được cấu hình để chỉ cho phép các thiết bị trong phần đó truy cập vào các dịch vụ mạng cụ thể, giúp tăng hiệu suất mạng.

Trong tổ chức, các phòng ban khác nhau có thể được phân chia thành các VLAN khác nhau. Mỗi VLAN có thể được xác định bằng một số cổng trên switch, hoặc theo địa chỉ MAC hoặc địa chỉ IP của các thiết bị trong VLAN.


Ứng dụng VLAN còn cho phép các tổ chức phân chia mạng thành các khu vực độc lập để phù hợp với mục đích sử dụng của từng khu vực. Ví dụ, trong một khu vực sản xuất, các thiết bị và người dùng chỉ được phép truy cập vào các tài nguyên trong khu vực đó để đảm bảo an toàn và bảo mật.

VLAN cũng cho phép các tổ chức cấu hình các thiết bị mạng khác nhau để hoạt động trong cùng một VLAN. Ví dụ, các thiết bị có thể bao gồm máy tính, điện thoại IP, camera an ninh và thiết bị IoT. Các thiết bị này có thể được phân bổ vào cùng một VLAN để cho phép chúng giao tiếp và chia sẻ tài nguyên mạng.

Các loại VLAN khác nhau bao gồm:

- Port-based VLAN: Sử dụng cổng trên switch để phân chia các thiết bị vào các VLAN khác nhau.

- Tag-based VLAN: Sử dụng các tag VLAN để phân chia các thiết bị vào các VLAN khác nhau. Tag VLAN được sử dụng để đánh dấu các gói tin dữ liệu để cho phép các switch định tuyến gói tin đến các VLAN khác nhau.

- Protocol-based VLAN: Sử dụng các loại giao thức để phân chia các thiết bị vào các VLAN khác nhau. Ví dụ, các giao thức như IP, IPX và AppleTalk có thể được sử dụng để phân chia các thiết bị vào các VLAN khác nhau.

- VLAN số: Sử dụng các số VLAN để phân chia các thiết bị vào các VLAN khác nhau. VLAN số được đánh số từ 1 đến 4094, trong đó các VLAN từ 1 đến 1005 được coi là VLAN tiêu chuẩn, và các VLAN từ 1006 đến 4094 được coi là VLAN mở rộng.

Tóm lại, VLAN là một công nghệ quan trọng trong việc quản lý mạng nội bộ, cho phép các tổ chức phân chia mạng thành các phần khác nhau để kiểm soát quyền truy cập của các thiết bị và người dùng. VLAN cũng cho phép các thiết bị mạng khác nhau hoạt động trong cùng một VLAN để giao tiếp và chia sẻ tài nguyên mạng. Có nhiều loại VLAN khác nhau có thể được sử dụng, bao gồm port-based, tag-based, protocol-based và VLAN số.