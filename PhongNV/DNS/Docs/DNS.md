# ***Tìm hiểu về DNS***
## ***1. DNS là gì***
![ima](../IMG/1.png)
DNS, viết tắt của Domain Name System, được hiểu là hệ thống phân giải tên miền. Nghĩa là, đây là một hệ thống chuyển đổi các tên miền website, chuyển từ dạng www.tenmien.com sang dạng địa chỉ IP tương ứng với tên miền và ngược lại. Bên cạnh đó, các thao tác này có DNS có vai trò lớn trong liên kết các thiết bị mạng với nhau trong việc định vị và gán địa chỉ cụ thể cho các thông tin trên internet.
Hệ thống phân giải tên miền giúp truy cập vào địa chỉ IP của website mà bạn muốn dễ dàng và nhanh chóng hơn. Hiểu đơn giản, DNS giống như danh bạ điện thoại, trong đó, địa chỉ IP tương ứng với số điện thoại còn tên miền của website tương ứng với tên chủ nhân số điện thoại đó.
## ***2. Kiến trúc của DNS***
- Không gian tên miền (Domain name space)
- Tên miền (Domain name)
- Cú pháp tên miền (Domain name syntax)
- Tên miền quốc tế hóa (Internationalized domain names)
- Máy chủ tên miền (Name servers)
- Máy chủ tên miền có thẩm quyền (Authoritative name server)
## ***3. Chức năng của DNS Server***

Chức năng của DNS được ví như một ” thông dịch viên” cùng với chức năng truyền đạt thông tin. DNS chuyển tên miền thành địa chỉ IP bao gồm 4 nhóm số khác nhau. 
Các địa chỉ IP dùng để định danh tài nguyên mạng. Khi kết nối với mạng Internet, mỗi địa chỉ IP sẽ được gán cho một máy tính. Hệ thống phân giải domain giúp chuyển đổi những địa chỉ IP thành những ký tự dễ hiểu hơn. DNS có những chức năng sau:

- Mỗi hệ thống phân giải  tên miền có chức năng ghi nhớ domain mà nó đã phân giải và ưu tiên cho những lần truy cập tiếp theo.
- Người dùng có thể sử dụng rất nhiều dịch vụ mạng như xem phim, tìm kiếm thông tin, chơi game, đăng nhập các website,… Nếu không có hệ thống phân giải tên miền DNS thì con người không thể truy cập internet dễ dàng và nhanh chóng
## ***4. Các loại DNS Server***
- `DNS Recursor`: Bạn có thể hiểu DNS Recursor giống như một thủ thư, khi bạn truy cập 1 trang web, browser sẽ nhờ "thủ thư" tìm hộ địa chỉ IP, "thủ thư" sẽ đảm nhận việc đi tìm địa chỉ IP và trả về kết quả cho client. Để tìm địa chỉ IP thì thủ thư sẽ dùng các DNS server . Ngoài ra thì DNS Recursor sẽ có cơ chế cache để tăng tốc độ phản hồi thay vì lúc nào cũng đi tìm IP.
- `Root Name Server`: Là nơi xử lý bước đầu tiên trong việc dịch (phân giải) các tên máy chủ thành địa chỉ IP. Nó có thể được coi giống như một mục lục trong thư viện trỏ đến các giá sách khác nhau - đóng vai trò như một tham chiếu đến các DNS Server khác. Vd: Ta request địa chỉ IP của google.com thì Root name server sẽ trả về IP máy chủ DNS của .com (TLD Nameserver)
- `TLD Name Server` (Top level domain name server): Có thể được coi như một giá sách cụ thể trong thư viện. Máy chủ định danh này là bước tiếp theo trong quá trình tìm kiếm địa chỉ IP cụ thể và nó lưu trữ phần cuối cùng của tên máy chủ (Vd google.com, máy chủ TLD sẽ trả về IP của DNS chứa .google”).
- `Authoritative Name Server`: Có thể được coi như một cuốn từ điển trên giá sách. Là điểm dừng cuối cùng trong truy vấn địa và sẽ trả về địa chỉ IP của tên miền được yêu cầu cho DNS Recursor.

## ***5. Cách hoạt động***
Để hiểu rõ ta sẽ cùng đi tìm hiểu từng bước thực hiện phân giải tên miền
- Người dùng nhập "google.com" vào browser. Truy vấn sẽ được truyền vào Internet và được nhận bởi DNS Recursor
- DNS Recursor sẽ gửi truy vấn tới Root Name Server (.)
- Root Name Server sẽ trả về địa chỉ IP của TLD Name Server ( ở đây sẽ là .com TLD)
- DNS Recursor tiếp tục gửi truy vấn tới .com TLD
- .com TLD sẽ phản hồi bằng địa chỉ IP của google.com Authoritative Name Server
- DNS Recursor lại gửi truy vấn tới google.com Authoritative Name Server
- google.com Authoritative Name Server sẽ trả về địa chỉ IP của google.com cho DNS Recursor
- DNS Recursor phản hồi lại browser địa chỉ IP của tên miền được yêu cầu Sau khi thực hiện 8 bước trên thì browser đã có thể thực hiện request rồi.
- Browser thực hiện HTTP Request đến địa chỉ IP vừa truy vấn xong
- Server response dữ liệu về cho browser

# ***Tài liệu tham khảo***
<https://viblo.asia/p/dns-la-gi-va-cach-thuc-hoat-dong-cua-no-3Q75w7kB5Wb>
<https://fptcloud.com/dns-la-gi/>
<https://www.bkns.vn/dns-la-gi.html>


