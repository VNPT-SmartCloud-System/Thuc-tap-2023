# 1. Giới thiệu  
Khi chia một mạng lớn thành các VLAN nhỏ hơn, vòng lặp có thể xảy ra nếu các switch trong mạng VLAN được kết nối với nhau thông qua nhiều đường kết nối, tạo ra nhiều đường đi giữa các switch. Trong trường hợp này, các gói tin có thể đi qua cùng một đường đi nhiều lần, gây ra vòng lặp và gây ảnh hưởng đến hiệu suất của mạng.

![stp](img/STP(1).png)

Ví dụ, giả sử một mạng VLAN được chia thành hai VLAN, VLAN A và VLAN B, và có hai switch, Switch A và Switch B. Switch A và Switch B được kết nối với nhau thông qua hai đường kết nối vật lý. Khi một gói tin từ VLAN A gửi đến VLAN B, nó có thể đi qua cả hai đường kết nối giữa hai switch, tạo ra một vòng lặp.

Để ngăn chặn vòng lặp trong mạng VLAN, cần sử dụng các giao thức như ***STP (Spanning Tree Protocol)***. STP cho phép switch chọn một đường đi tối ưu giữa các switch trong mạng VLAN và loại bỏ các đường đi không cần thiết để tránh vòng lặp. STP sẽ chọn một switch làm Root Bridge và đánh giá tất cả các đường đi từ các switch khác đến Root Bridge. Sau đó, STP sẽ chọn một đường đi tối ưu cho mỗi switch trong mạng VLAN và loại bỏ các đường đi không cần thiết.
>**Root Bridge**: Là switch có Bridge ID thấp nhất trong mạng VLAN và được chọn làm điểm gốc để xác định đường đi tối ưu hóa cho các switch khác trong mạng.
# 2.  Spanning là gì ?
- STP là viết tắt của "Spanning Tree Protocol", là một giao thức mạng được sử dụng để đảm bảo rằng một mạng có cấu trúc liên kết phù hợp và tránh được vấn đề lặp lại khó khăn. STP có thể được sử dụng để duy trì tính toàn vẹn của các mạng LAN bằng cách loại bỏ các vòng lặp trong mạng.
- Theo mô hình, thì nó sẽ xảy ra hiện tượng  
  - **Broadcast storm(bão quảng bá)**
  ![stp](img/STP(2).png)

    Bão quảng bá (broadcast storm) là hiện tượng xảy ra khi có quá nhiều gói tin quảng bá được gửi trên một mạng. Khi một gói tin được gửi đến tất cả các thiết bị trong mạng, các thiết bị đó sẽ xử lý gói tin đó và tiếp tục gửi tiếp gói tin đến tất cả các thiết bị khác. Nếu có quá nhiều gói tin quảng bá được gửi liên tục, các thiết bị trong mạng sẽ phải xử lý rất nhiều gói tin, gây ra sự chậm trễ và có thể làm cho mạng trở nên không hoạt động.
  
    Bão quảng bá thường xảy ra khi có lỗi cấu hình trong mạng hoặc khi có virus hoặc malware tấn công mạng. Ví dụ, nếu một switch được cấu hình sai địa chỉ MAC của một thiết bị, switch có thể gửi các gói tin quảng bá đến tất cả các thiết bị trong mạng, dẫn đến bão quảng bá.
  - **Instability MAC address table(bảng MAC không ổn định)**
 là một hiện tượng xảy ra khi bảng địa chỉ MAC trên một switch bị thay đổi liên tục hoặc không đồng bộ với các switch khác trong mạng. Khi điều này xảy ra, switch không thể xác định đường đi chính xác để chuyển tiếp các gói tin, dẫn đến lỗi kết nối và giảm hiệu suất của mạng.
  - **Multiple Frame copies(đa bản sao cùng một frame)**

  ![stp](img/STP(3).png)

     MFC xảy ra khi một khung dữ liệu (frame) được nhân bản và gửi đến nhiều thiết bị khác nhau trong mạng. Tình trạng này gây lãng phí tài nguyên mạng và làm giảm hiệu suất mạng.


- Hiện tượng loop xảy ra khi các sw đấu nối theo 1 vòng khép kin 
- IEEE đưa ra chuẩn 802.1D(Spanning Tree Protocol) để chống loop
# 3. Tiến trình bầu chọn và hoạt động của Giao thức Spanning Tree
Hoạt động bàu chọn của một tiến trình STP
- Thực hiện bầu chọn Root-Bridge
- Bầu chọn Root-Port
- Lựa chọn các Designated-port
- Blocking các port còn lại

## 3.1 Bầu chọn Root-Bridge
![stp](img/STP(4).png)
- Khi các switch được đấu nối khởi động nó sẽ gửi gói tin BPDU (bridge protocol data unit) trên các port của switch
- Thông số quyết định sw nào được làm Root sw là Bridge-ID( 8byte) gồm có các thông số  
  - Priority (của switch)
    - Dài 2 byte: có giá trị từ 0 - 65535 default = 32768
    - Switch nào có số priority có chỉ số nhỏ nhất sẽ được chọn là Root-Switch
  - MAC address switch 
    - Dài 6 byte 
    - Xét từ trái sang phải từng giá trị hexa thì switch nào có MAC nhỏ nhất làm Root-Switch

Tiến trình bầu chọn Root-Bridge sẻ tiến hành như sau:
- Đầu tiên sẻ so sánh Sw nào có số Priority thấp nhất sẻ là Root-Bridge
- Các Sw được thiết lập số Priority bằng nhau thì tiến trình thứ 2 là so sánh MAC sẻ thực hiện, Sw nào có MAC nhỏ nhất sẻ làm Root-Bridge. MAC là địa chỉ duy nhất trên thế giới nên sẻ không xảy ra trùng lập được. VD như hình trên SW1 có MAC nhỏ nhất nên sẻ được bầu chọn làm Root-Bridge.
- Sau khi đã bầu chọn được Root-Bridge thì chỉ có SW làm root mới gửi BPDU ra khỏi cổng để duy trì tiến trình STP ( gửi 2s/lần). Các SW con chỉ nhận, bổ xung thông tin BPDU và forward thông tin BPDU này.

    ![stp](img/STP(5).png)


## 3.2 Bầu chọn Root port

- Là port cung cấp đường về root-switch  mà có tổng path-cost nhỏ nhất
- Khi bầu chọn Root-switch thì Root-switch không tham  gia quá trình bàu chọn này  
- Mỗi non-root-switch  chỉ có một root-port 
- Path-cost là giá trị cost trên từng cổng của switch

Bandwidth | cost
---|---
10 Mbps| 100 
100 Mbps | 19
1 Gbps | 4
10 Gbps |2

- Nguyên tắc tính tổng path-cost: tính từ root-switch đến switch đang muốn tính  
  - Đi vào: cộng cost
  - Đi ra: không cộng

  ![stp](img/STP(6).png)

- Luật Tie-Break: sử dụng khi port  sw có  path-cost bằng nhau
  - Sender Bridge ID:
    - Cổng nào kết nối switch mà sw có bridge id nhỏ nhất -> port đó được chọn  làm root-port
  - Sender Port ID:
    - Port ID của Switch bên kia thì port nào của switch bên kia có giá trị port-ID nhỏ hơn thì chọn port bên switch mình kết nối với port ID nhỏ hơn đó.
      - **Priority của port**: có giá trị từ 0 -> 255, default=128. Port nào có priority nhỏ hơn thì port đó có Port ID nhỏ hơn.
      - **Vị trí của port**: Xét theo hạng của số thứ tự của port. Port số 1 < port 2 -> port số 1 làm root-port

- Khi các luật trên không giải quyết được thì nó sẽ xét đến Port ID trên chính nó
  - Priority và vị trí của port
## 3.3 Bầu chọn Designated port
- Tất cả port của root-switch đều là Designated port
- Trên 1 phân đoạn nếu port đối diện là root-port thì mình là Designated port(không có nghĩa ngược lại)
- Là port cung cấp đường về Root-switch trên phân đoạn mạng đang xét mà có tổng path-cost là nhỏ nhất

    ![stp](img/STP(7).png)

VD: Port e0/3 của SW3 trên phân đoạn mạng giữa SW3 và SW4 có tổng cost là 100, e0/3 của SW4 có tổng cost 200 nên e0/3 SW3 sẻ thành Designated port

## 3.4 Bầu chọn Block port (Alternate port, port bị khóa)
- Khi một trong các phân đoạn khác bị đứt thì phân đoạn port block sẽ được mở ra để chạy  
- Khi phân đoạn  trên có lại thì phân đoạn block sẽ tiếp tục block lại
- Tuy port block không nhận được dữ liệu nhưng nó vấn nhận gói tin BPDU tù Root-switch để duy trì cây spanning-tree
- Kết quả sau 4 bước bầu chọn , cây STP hội tụ như sơ đồ sau  


## 3.5 STP timer
STP sử dụng các định thời : hello timer, forward delay timer, max age timer.
- Helo timer: default 2s. Khoảng thời gian mà Root-bridge tiến hành gửi các gói tin BPDU ra khỏi cổng của nó để duy trì tiến trình STP.
- Forward delay timer: default là 15s. Thời gian các trạng thái Listening. Learning trước khi sang Forwarding để hội tụ.
- Max-age times: default là 20s. Khi một cổng đang tiến hành nhận BPDU và đột nhiên nhận một BPDU kém hơn(inferior BPDU). Port này sẻ chờ hết thời gian Max-age timer rồi mới thực hiện các hoạt động hội tụ mạng.
Nếu Root-Switch chết hay port block không nhận được BPDU thì mất 20s nó mới hoạt động 
## 5.6  STP status 
Các trạng thái trong một tiến trình STP đến khi hội tụ bao gồm:
- Disable: cổng này đang ở trạng thái không active.
- Blocking: port đang bị khóa Alternated port. Chỉ tiếp nhận BPDU mà không cho BPDU đi ra khỏi cổng. Không học địa chỉ MAC vào bảng MAC và không forward được dữ liệu.
- Listening: có đặc tính cổng chỉ nhận BPDU hoặc gửi BPDU. Không học địa chỉ MAC vào bảng MAC và không forward được dữ liệu
- Leaning: giống như trạng thái Listenning cổng chỉ nhận BPDU hoặc gửi BPDU. Có thể học được địa chỉ MAC vào bảng MAC và không forward được dữ liệu.
- Forwarding: cổng chỉ nhận BPDU hoặc gửi BPDU.  Tương tự Learning có thể học địa chỉ MAC vào bảng MAC và có thể forward được dữ liệu.

# **Tài Liệu Tham Khảo**

https://itforvn.com/tu-hoc-ccnax-bai-7-spanning-tree.html/
