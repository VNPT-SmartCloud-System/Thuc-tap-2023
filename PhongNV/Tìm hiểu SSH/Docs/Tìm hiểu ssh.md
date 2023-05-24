# ***Tìm hiểu về SSH***
## ***SSH là gì và cơ chế hoạt động***
### ***Giới thiệu***
 SSH (secure shell) là một giao thức mã hóa dùng để quản 
trị và giao tiếp với servers.
- SSH hoạt động ở lớp trên trong mô hình phân lớp TCP/IP
- Các công cụ SSH (như là OpenSSH, PuTTy,…) cung cấp cho 
người dùng cách thức để thiết lập kết nối mạng được mã 
hoá để tạo 1 kênh kết nối riêng tư.
- Hơn nữa tính năng tunneling (hoặc còn gọi là port 
forwarding) của các công cụ này cho phép chuyển tải các 
giao vận theo các giao thức khác.
- Mỗi khi dữ liệu được gửi bởi 1 máy tính vào mạng, SSH 
tự động mã hoá nó. Khi dữ liệu được nhận vào, SSH tự động 
giải mã nó.
- Kết quả là việc mã hoá được thực hiện trong suốt.

Có một vài cách để SSH tới SSH server như dùng password 
hoặc keypair. Trong đó phương thức dùng keypair được cho 
là có tính bảo mật cao hơn bởi nếu trong quá trình sử 
dụng mà các gói tin của bạn bị bắt lại, các phiên trao 
đổi khóa giữa SSH server và Client sẽ bị lộ và attacker 
có thể dùng nó để giải mã dữ liệu. Hơn nữa, việc này cũng 
tạo điều kiện cho các cuộc tấn công Brute Force mật khẩu.

SSH có hỗ trợ sử dụng cặp khóa Private Key và Public Key 
được chia sẻ với nhau từ trước. Nghĩa là bạn đã có sẵn 
Private Key để trao đổi với server mà không cần đến quá 
trình trao đổi khóa, điều này sẽ hạn chế khả năng bị bắt 
gói. Hơn nữa cặp khóa này còn có một mật khẩu riêng của 
nó, gọi là passphrase (hay keyphrase). Mật khẩu này được 
dùng để mở khóa Private Key (được hỏi khi bạn SSH vào 
server) và tạo lớp xác thực thứ 2 cho bộ khóa. Nghĩa là:
- Nếu attacker không có Private Key, việc truy cập vào 
server gần như không thể, chỉ cần bạn giữ kĩ Private Key.
- Tuy nhiên trong trường hợp Private Key bị lộ, bạn vẫn 
khá an toàn vì đối phương không có passphrase thì vẫn 
chưa thể làm được gì, tuy nhiên đó chỉ là tạm thời. Bạn 
cần truy cập server thông qua cách trực tiếp hoặc qua VNC 
của nhà cung cấp nếu đó là một VPS để thay đổi lại bộ 
khóa.

### ***Khái niệm***
SSH viết đầy đủ là Secure Shell, đây là một giao thức hỗ 
trợ các nhà quản trị mạng truy cập vào máy chủ từ xa 
thông qua địa chỉ ip . Ngoài ra, SSH còn cung cấp các bộ 
tiện ích phục vụ phát triển chính giao thức SSH.
SSH tạo ra cơ chế xác thực qua mật khẩu mạnh, hình thành 
mối liên kết giao tiếp dữ liệu mã hóa ra giữa hai máy qua 
môi trường internet. Ngày nay giao thức SSH được giấy 
quản trị mạng sử dụng phổ biến trong quá trình quản lý, 
điều chỉnh ứng dụng từ xa. Nó cho phép vị tự đăng nhập 
vào mạng máy tính và thực hiện một số tác vụ cơ bản như 
dịch chuyển file.
### ***Cơ chế hoạt động***
 Một phiên làm việc của SSH đều phải trải qua 4 bước:

- Thiết lập kết nối ban đầu (SSH-TRANS)
- Tiến hành xác thực (SSH-AUTH)
- Mở phiên kết nối để thực hiện các dịch vụ (SSH-CONN)
- Chạy các ứng dụng SSH (Có thể là SSH-SFTP, SCP)

SSH-TRANS: là khối xây dựng cơ bản cung cấp kết nối ban 
đầu, ghi chép giao thức, xác thực server, mã hóa cơ bản 
và bảo toàn dữ liệu. Sau khi thiết lập kết nối, client có 
một kết nối độc lập và bảo mật

Sau đó, client dùng SSH-AUTH để xác thực đến server. 
SSH-AUTH yêu cầu một phương thức: Public key với thuật 
toán DSA. Ngoài ra, sử dụng mật khẩu và hostbased

Sau khi xác thực, SSH client yêu cầu SSH-CONN để cung cấp 
một kênh riêng biệt qua SSH-TRANS

Ngoài ra, còn cung cấp các dịch vụ như Remote Login and 
Command Execution, agent fowarding, files transfer, TCP 
port fowarding, X fowarding,...

Cuối cùng, một ứng dụng có thể sử dụng SSH-SFTP hoặc SCP 
truyền file hoặc thao tác remote từ xa
   
### ***Các chức năng chính***
Giao thức đảm nhiệm khá nhiều chức năng trong hệ thống 
điều khiển, liên kết máy chủ. Các chức năng cơ bản phải 
kể đến như:

- Hỗ trợ truy cập từ xa vào những hệ thống, thiết bị ứng 
dụng giao thức SSH
- Cho phép dịch chuyển file an toàn
- Thực thi lệnh bảo mật, an toàn trên hệ thống điều khiển 
từ xa
- Quản lý an toàn và hiệu quả thành phần hạ tầng mạng

### ***Các thành phần trong SSH***
- **Server** : Một chương trình cho phép đi vào kết nối 
SSH với một bộ máy, trình bày xác thực, cấp phép, … Trong 
hầu hết SSH bổ sung của Unix thì server thường là sshd.
- **Client** : Một chương trình kết nối đến SSH server và 
đưa ra yêu cầu như là “log me in” hoặc “copy this file”. 
Trong SSH1, SSH2 và OpenSSH, client chủ yếu là ssh và scp.
- **Session** : Một phiên kết nối giữa một client và một 
server. Nó bắt đầu sau khi client xác thực thành công đến 
một server và kết thúc khi kết nối chấm dứt. Session có 
thể được tương tác với nhau hoặc có thể là một chuyến 
riêng.

## ***Tìm hiểu các tùy chọn cơ bản của file cấu hình SSH***

 
### ***1. Khởi tạo phiên SSH***
- Nếu đang sử dụng Linux hoặc Mac OS , kết nối SSH khá 
đơn giản bằng cách sử dụng Terminal . Nếu sử dụng 
Windows , cần thêm 1 chương trình khác để mở kết nối 
SSH . Trình kết nối SSH được sử dụng phổ biến nhất cho 
Windows là PuTTY .
- Với Mac OS và Linux , mở Terminal và gõ lệnh theo cấu 
trúc sau :
    ```
    # ssh user@[host/IP]
    ```
- Trong đó :
    - `user` : user local trên máy cần ssh
    - `host/IP` : hostname ( VD : `www.xyzdomain.com` ) 
hoặc IP của máy cần kết nối SSH ( VD : `244.235.23.
19` )
- Sau khi thực hiện lệnh , máy đầu xa sẽ yêu cầu password 
của user sử dụng SSH .

