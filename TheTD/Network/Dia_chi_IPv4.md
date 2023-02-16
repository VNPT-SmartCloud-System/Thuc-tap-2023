# **Địa chỉ IPv4**
## **Giới thiệu về IPv4**
Giao thức IP là một giao thức của chồng giao thức TCP/IP thuộc tầng mạng.

Internet Protocol version 4 (IPv4 là một trong hai loại giao thức Internet Protocol (IP) được sử dụng để định danh các thiết bị trong mạng Internet. IPv4 sử dụng địa chỉ 32-bit được chia thành 4 octet (hay 4 nhóm 8-bit), mỗi octet được biểu diễn bằng số thập phân từ 0 đến 255. Các địa chỉ IPv4 được sử dụng trong mạng Internet được phân bố và quản lý bởi các tổ chức chuyên trách trên toàn cầu.
## **Đặc điểm**
- Là một trong những giao thức quan trọng nhất của bộ giao thức TCP/IP.
- Là giao thức hướng không liên kết (Connectionless): Dữ liệu của IP được truyền đi ngay lập tức nếu có thể (best effort), không có bất kỳ cơ chế thiết lập kết nối, không có cơ chế báo nhận hay điều khiển luồng nào được sử dụng với IP, các gói tin IP cũng không được đánh số thứ tự khi trao đổi trên mạng.
- Mỗi gói tin IP sử dụng cơ chế xác định địa chỉ theo kiểu phân cấp, trong đó phần `Network ID` của địa chỉ giống như tên của một con đường và phần `Host ID` của địa chỉ sẽ là số nhà của một căn nhà trên con đường ấy.
- Không có cơ chế khôi phục lại gói tin bị mất trên đường truyền. Việc này được giao lại cho các giao thức tầng trên để đảm bảo độ tin cậy.
## **Cấu trúc gói tin**
Gồm 2 phần là `Header` và `Data`. Header chứa thông tin quản lý của gói tin, Dât là phần dữ liệu cần truyền tải được đóng gói trong IP
![ipv4](img/IPv4(1).png)

- **Version(4 bit)**: chỉ ra phiên bản hiện hành của IP đang được dùng. Nếu trường này khác với phiên bản IP của thiết bị nhận, thiết bị nhận sẽ từ chối và loại bỏ các gói tin này
- **IP Header Length (4 bit)**: Chiều dài gói tin IP Header
- **Service Type (8 bit)**:
Đánh dấu dữ liệu (Marking) phục vụ cho tác vụ QoS với các gói tin IP.

   - **QoS (Quality of Service)** là tập hợp các kỹ thuật cho phép cấp phát tài nguyên một cách thích hợp cho cá loại dữ liệu khác nhau, từ đó có thể đảm bảo chất lượng dịch vụ mạng cho các loại dữ liệu này
- **Precedence (3 bit)**: chỉ thị quyền ưu tiên gửi datagram, cụ thể:

    |**Priority**|**Main|
    |------------|------|
    |111|Network Control (cao nhất)|
    |011|Flash|
    |110|Internetwork Control|
    |010|Immediate|
    |101|CRITIC/ECP|
    |001|Prioty|
    |100|Flash Override|
    |000|Routine (Thấp nhất)|
- **Delay (1 bit)**: Chỉ độ trễ yêu cầu. 0: Thông lượng bình thường; 1: Thông lượng cao.
- **Throughput (1 bit)**: Chỉ số thông lượng yêu cầu. 0: Thông lượng bình thường; 1: Thông lượng cao.
- **Reliability (1 bit)**: Chỉ độ tin cậy yêu cầu. 0: Độ tin cậy bình thường; 1: Độ tin cậy cao.
- **Total Lenght (16 bit)**: chiều dài của toàn bộ gói tin IP kể cả phần Header được tính theo byte. Để biết chiều dài của dữ liệu cần lấy tổng chiều dài này trừ đi HL.
- **Identification (16 bit)**: Trường định danh, cùng các tham số khác như địa chỉ nguồn (Source address) và địa chỉ đích (Destination address) để định danh duy nhất cho mỗi Datagram được gửi đi bởi 1 trạm. Thông thường phần định danh được tăng thêm 1 khi 1 Datagram được gửi .
- **Flag (3 bit)**: Cờ được sử dụng trong khi phân đoạn các Datagram.
    - *Bit 0*: Reserved chưa sử dụng, giá trị luôn là 0.
    - *Bit 1*: DF = 1: Gói tin bị phân đoạn, có nhiều hơn 1 đoạn, DF = 0: Gói tin không bị phân đoạn.
    - *Bit 2*: MF  = 0: Đoạn cuối cùng, MF = 1: chưa là đoạn cuối cùng, còn đoạn khác phía sau nữa.
    - **MTU (Maximum Transmission Unit)** là kích thước dữ liệu tối đa mà một gói tin được phép mang trên một mạng. Trong IPv4, MTU được quy định là 1500 byte, tuy nhiên, kích thước này có thể thay đổi tùy thuộc vào các thiết bị mạng và đặc tính của mạng.

        Khi một gói tin được truyền qua một mạng, nó sẽ được chia thành các phần nhỏ hơn được gọi là các gói tin con. Kích thước của các gói tin con này phụ thuộc vào kích thước MTU của mạng. Nếu kích thước của một gói tin vượt quá MTU của mạng, gói tin sẽ bị chia thành các phần nhỏ hơn và truyền qua mạng dưới dạng các gói tin con riêng lẻ. Quá trình này được gọi là fragmentation.
        
        Tuy nhiên, fragmentation có thể dẫn đến hiệu suất kém và tăng độ trễ trên mạng. Vì vậy, các thiết bị mạng sẽ cố gắng tránh fragmentation bằng cách điều chỉnh kích thước của gói tin để phù hợp với MTU của mạng.
        - **Fragmentation** là quá trình chia nhỏ một gói tin lớn thành các phần nhỏ hơn để truyền qua các mạng có kích thước MTU khác nhau. Tuy nhiên, quá trình này có thể dẫn đến hiệu suất kém và tăng độ trễ trên mạng vì các lý do sau:
        1. Tăng độ trễ: Khi một gói tin bị chia nhỏ, các phần con sẽ được gửi qua mạng một cách độc lập. Khi các phần con này đến đích, chúng sẽ phải được ghép lại để tái tạo lại gói tin ban đầu. Việc này tốn thời gian và tăng độ trễ trên mạng.
        2. Mất gói tin: Nếu một trong các phần con bị mất hoặc không được gửi đến đích, gói tin sẽ không thể tái tạo lại và sẽ bị mất hoàn toàn. Điều này có thể xảy ra do vấn đề về đường truyền, hoặc do các thiết bị trên đường truyền không hỗ trợ fragmentation.
        3. Hiệu suất kém: Khi các gói tin bị chia nhỏ và gửi qua mạng dưới dạng các phần con, các phần con này có thể phải chuyển đổi lại thành các gói tin ban đầu trước khi được xử lý bởi các thiết bị đích. Quá trình chuyển đổi này có thể tốn nhiều thời gian và tài nguyên, gây ra hiệu suất kém trên mạng.


- **Fragment Offset (13 bit)**: Chỉ vị trí của đoạn phân mảnh (Fragment) trong IP Datagram tính theo đơn vị 64 bit.
- **Time to Live (8 bit)**: Sử dụng để chống loop gói tin IP khi xảy ra lỗi định tuyến trên sơ đồ mạng. Giá trị này được đặt lúc bắt đầu gửi gói tin và nó sẽ giảm đi 1 đơn vị khi đi qua 1 router. Khi TTL = 0, gói tin sẽ bị loại bỏ.
- **Protocol (8 bit)**: Nhận dạng giao thức nào đang được truyền tải trong phần data của gói tin IP, như TCP hay UDP.
- **Header checksum (8 bit)**: Kiểm tra lỗi của IP Header. Nếu như việc kiểm tra này thất bại, gói dữ liệu sẽ hủy bỏ tại nơi xác định được lỗi.
- **Source Address (32 bit)**: Địa chỉ của trạm nguồn.
-  **Destination Address (32 bit)**: địa chỉ của trạm đích.
- **Option (Có độ dài thay đổi)**: cho phép thêm vào tính năng mới cho giao thức IP.
- **Padding (Độ dài thay đổi)**: Cấu trúc của gói IP quy định option phải là bội số của 32 bit nên nếu option không đủ số bit, các bit padding sẽ được thêm vào để đạt được yêu cầu này.
- **Data (độ dài thay đổi)**: vùng dữ liệu có độ dài là bội của 8 bit, tối đa là 65535 byte.

## **Cấu trúc địa chỉ**
Địa chỉ IPv4 được sử dụng để định danh cho các thiết bị mạng Internet. Địa chỉ mạng này được biểu diễn dưới dạng 32 bit, được chia thành 4 nhóm 8 bit (gọi là octet) và mỗi nhóm được biểu diễn dưới dạng số thập phân trong khoảng từ 0-255, mỗi octet ngăn nhau bởi dấu chấm.

**Cấu trúc địa chỉ IPv4** bao gồm 2 phần chính: Phần mạng (network) và phần máy chủ (host). phần mạng xác định mạng nào mà thiết bị đó thuộc về, còn phần máy chủ xác định địa chỉ của thiết bị đó trên mạng đó. 

![ipv4](img/ipv4(2).png)

**Các dạng địa chỉ**
- **Địa chỉ mạng (Network Address)**
    - Định danh cho một mạng
    - Tất cả các bit phần HostID là 0
- **Địa chỉ quảng bá (Broadcast Address)**
    - Địa chỉ dùng để gửi dữ liệu cho tất cả các máy tính trong mạng
    - Tất cả các bit phần HostID là 1
- **Địa chỉ máy trạm (Unicast Address)**: Gán cho một cổng mạng
- **Địa chỉ nhóm (Multicast address)**: Định danh cho nhóm

**Các lớp địa chỉ**

![ipv4](img/ipv4(3).png)

**Lớp A**

    Lớp A được sử dụng cho các mạng lớn với nhiều host. Lớp A sử dụng 8 bit đầu tiên để xác định mạng và 24 bit cuối để xác định host. Địa chỉ IP lớp A có dạng x.y.z.w, trong đó giá trị của x nằm trong khoảng từ 1-126
**Lớp B**

    Lớp B được sử dụng cho các mạng trung bình với số lượng host trung bình. Lớp B sử dụng 16 bit đầu tiên để xác định mạng và 16 bit cuối để xác định host. Địa chỉ IP lớp B có dạng x.y.z.w, trong đó giá trị của x nằm trong khoảng từ 128 đến 191.
**Lớp C**

    Lớp C được sử dụng cho các mạng nhỏ với số lượng host ít. Lớp C sử dụng 24 bit đầu tiên để xác định mạng và 8 bit cuối để xác định host. Địa chỉ IP lớp C có dạng x.y.z.w, trong đó giá trị của x nằm trong khoảng từ 192 đến 223.

**Lớp D**

    Lớp D được sử dụng để định danh cho các multicast address (địa chỉ đa điểm). Lớp D sử dụng 4 bit đầu tiên để đánh dấu địa chỉ multicast và 28 bit còn lại để xác định địa chỉ mạng.

**Lớp E**

    Lớp E được dành riêng cho các mục đích thử nghiệm và nghiên cứu. Lớp E sử dụng 5 bit đầu tiên để đánh dấu địa chỉ và 27 bit còn lại để xác định địa chỉ mạng.

## **IP public, IP Private, IP tĩnh và động**
1. **Địa chỉ IP public**:
Địa chỉ IP public là địa chỉ được cung cấp bới ISP (Nhà cung cấp dịch vụ Internet) cho cá thiết bị kết nối trực tiếp với Internet, như máy chủ web, máy chủ email, máy tính cá nhân có sử dụng dịch vụ đám mây,... Địa chỉ IP public cho phép các thiết bị này có thể truy cập từ mọi nơi trên Internet.

![ipv4](img/ipv4(4).png)


2. **Địa chỉ Ip private**:
Địa chỉ IP private là địa chỉ được sử dụng bên trong mạng nội bộ, không sử dụng kết nối trực tiếp với Internet. Các địa chỉ IP private thường được sử dụng trong mạng gia đình hoặc mạng doanh nghiệp và các thiết bị kết nối vào mạng cục bộ sẽ được cấp phát địa chỉ IP private để sử dụng. Các thiết bị kết nối vào Internet thông qua một thiết bị trung gian như modem hoặc router, sẽ có địa chỉ IP public được cấp phát bởi ISP

![ipv4](img/IPv4(5).png)

3. **Địa chỉ IP tĩnh**:
Địa chỉ IP tĩnh là địa chỉ IP được cấp phát cố định cho một thiết bị kết nối vào mạng, nó không thay đổi theo thời gian. Địa chỉ IP tĩnh thường được sử dụng cho các máy chủ, các thiết bị yêu cầu sự ổn định và liên tục kết nối với mạng, như các hệ thống máy chủ, các thiết bị chuyên dụng.

4. **Địa chỉ IP động**:
Địa chỉ IP động là địac hỉ IP được cấp phát một cách tạm thời cho một thiết bị kết nối vào mạng, thường được quản lý bởi một máy chủ DHCP (Dynamic Host Configuration Protocol). Địa chỉ IP động thường được sử dụng cho các thiết bị trên mạng LAN và Internet

**NAT (Network Address Translation)**
Khi một mạng nội bộ sử dụng địa chỉ IP private và muốn kết nối với Internet, NAT sẽ được sử dụng để chuyển đổi địa chỉ IP private thành địa chỉ IP public và ngược lại. NAT thường được sử dụng trên modem hoặc router để cung cấp cho mạng nội bộ một địa chỉ IP public chung để truy cập Internet.

![ipv4](img/ipv4(6).png)

**CIDR (Classless Inter-Domain Routing)**
CIDR là một phương pháp phân loại địa chỉ IP dựa trên độ dài của địa chỉ mạng. CIDR cho phép chia địa chỉ IP thành các mạng con nhỏ hơn, dễ quản lý hơn và tận dụng tốt các địa chỉ IP. CIDR sử dụng prefix length để xác định độ dài của địa chỉ mạng.

**Subnetting**
 là một phương pháp chia một mạng lớn thành các mạng con nhỏ hơn, gọi là subnet. Subnetting giúp tăng hiệu suất mạng và giảm sự lãng phí địa chỉ IP. Trong subnetting, các bit được sử dụng để định danh địa chỉ mạng và địa chỉ con mạng được phân bổ trong một mạng lớn hơn.

## **Chia subnet mask**

 *Ví dụ*:
 Cho  192.168.1.100/27. Tìm địa chỉ mạng, subnetmask, dải host.

 ![ipv4](img/ipv4(7).jpg)
 
    Với n bit phần host, thì sẽ có 2^n-2 địa chỉ
    Địa chỉ mạng là tất cả các bit 0
    Địa chỉ cast là tất cả các bit 1
    Còn lại là địa chỉ host
## **Tài liệu tham khảo**
1. https://viblo.asia/p/tim-hieu-giao-thuc-ip-phan-1-bJzKmxer59N
2. https://viblo.asia/p/tim-hieu-giao-thuc-ip-phan-2-XL6lAMNmlek

3. https://bkaii.com.vn/tin-nganh-2/132-khai-niem-co-ban-ve-ip-ip-public-va-ip-private

4. https://vnpro.vn/thu-vien/chuong-1-dia-chi-ipv4-chia-subnet-vlsm-summary-4108.html