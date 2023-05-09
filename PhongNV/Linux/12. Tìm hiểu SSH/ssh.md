# ***Tìm hiểu về SSH***
## ***SSH là gì và cơ chế hoạt động***
### ***Giới thiệu***
 SSH (secure shell) là một giao thức mã hóa dùng để quản trị và giao tiếp với servers.
- SSH hoạt động ở lớp trên trong mô hình phân lớp TCP/IP
- Các công cụ SSH (như là OpenSSH, PuTTy,…) cung cấp cho người dùng cách thức để thiết lập kết nối mạng được mã hoá để tạo 1 kênh kết nối riêng tư.
- Hơn nữa tính năng tunneling (hoặc còn gọi là port forwarding) của các công cụ này cho phép chuyển tải các giao vận theo các giao thức khác.
- Mỗi khi dữ liệu được gửi bởi 1 máy tính vào mạng, SSH tự động mã hoá nó. Khi dữ liệu được nhận vào, SSH tự động giải mã nó.
- Kết quả là việc mã hoá được thực hiện trong suốt.

Có một vài cách để SSH tới SSH server như dùng password hoặc keypair. Trong đó phương thức dùng keypair được cho là có tính bảo mật cao hơn bởi nếu trong quá trình sử dụng mà các gói tin của bạn bị bắt lại, các phiên trao đổi khóa giữa SSH server và Client sẽ bị lộ và attacker có thể dùng nó để giải mã dữ liệu. Hơn nữa, việc này cũng tạo điều kiện cho các cuộc tấn công Brute Force mật khẩu.

SSH có hỗ trợ sử dụng cặp khóa Private Key và Public Key được chia sẻ với nhau từ trước. Nghĩa là bạn đã có sẵn Private Key để trao đổi với server mà không cần đến quá trình trao đổi khóa, điều này sẽ hạn chế khả năng bị bắt gói. Hơn nữa cặp khóa này còn có một mật khẩu riêng của nó, gọi là passphrase (hay keyphrase). Mật khẩu này được dùng để mở khóa Private Key (được hỏi khi bạn SSH vào server) và tạo lớp xác thực thứ 2 cho bộ khóa. Nghĩa là:
- Nếu attacker không có Private Key, việc truy cập vào server gần như không thể, chỉ cần bạn giữ kĩ Private Key.
- Tuy nhiên trong trường hợp Private Key bị lộ, bạn vẫn khá an toàn vì đối phương không có passphrase thì vẫn chưa thể làm được gì, tuy nhiên đó chỉ là tạm thời. Bạn cần truy cập server thông qua cách trực tiếp hoặc qua VNC của nhà cung cấp nếu đó là một VPS để thay đổi lại bộ khóa.

### ***Khái niệm***
SSH viết đầy đủ là Secure Shell, đây là một giao thức hỗ trợ các nhà quản trị mạng truy cập vào máy chủ từ xa thông qua mạng internet không bảo mật. Ngoài ra, SSH còn cung cấp các bộ tiện ích phục vụ phát triển chính giao thức SSH.
SSH tạo ra cơ chế xác thực qua mật khẩu mạnh, hình thành mối liên kết giao tiếp dữ liệu mã hóa ra giữa hai máy qua môi trường internet. Ngày nay giao thức SSH được giấy quản trị mạng sử dụng phổ biến trong quá trình quản lý, điều chỉnh ứng dụng từ xa. Nó cho phép vị tự đăng nhập vào mạng máy tính và thực hiện một số tác vụ cơ bản như dịch chuyển file.
### ***Cơ chế hoạt động***
 Một phiên làm việc của SSH đều phải trải qua 4 bước:

- Thiết lập kết nối ban đầu (SSH-TRANS)
- Tiến hành xác thực (SSH-AUTH)
- Mở phiên kết nối để thực hiện các dịch vụ (SSH-CONN)
- Chạy các ứng dụng SSH (Có thể là SSH-SFTP, SCP)

SSH-TRANS: là khối xây dựng cơ bản cung cấp kết nối ban đầu, ghi chép giao thức, xác thực server, mã hóa cơ bản và bảo toàn dữ liệu. Sau khi thiết lập kết nối, client có một kết nối độc lập và bảo mật

Sau đó, client dùng SSH-AUTH để xác thực đến server. SSH-AUTH yêu cầu một phương thức: Public key với thuật toán DSA. Ngoài ra, sử dụng mật khẩu và hostbased

Sau khi xác thực, SSH client yêu cầu SSH-CONN để cung cấp một kênh riêng biệt qua SSH-TRANS

Ngoài ra, còn cung cấp các dịch vụ như Remote Login and Command Execution, agent fowarding, files transfer, TCP port fowarding, X fowarding,...

Cuối cùng, một ứng dụng có thể sử dụng SSH-SFTP hoặc SCP truyền file hoặc thao tác remote từ xa
   
### ***Các chức năng chính***
Giao thức đảm nhiệm khá nhiều chức năng trong hệ thống điều khiển, liên kết máy chủ. Các chức năng cơ bản phải kể đến như:

- Hỗ trợ truy cập từ xa vào những hệ thống, thiết bị ứng dụng giao thức SSH
- Cho phép dịch chuyển file an toàn
- Thực thi lệnh bảo mật, an toàn trên hệ thống điều khiển từ xa
- Quản lý an toàn và hiệu quả thành phần hạ tầng mạng

### ***Các thành phần trong SSH***
- **Server** : Một chương trình cho phép đi vào kết nối SSH với một bộ máy, trình bày xác thực, cấp phép, … Trong hầu hết SSH bổ sung của Unix thì server thường là sshd.
- **Client** : Một chương trình kết nối đến SSH server và đưa ra yêu cầu như là “log me in” hoặc “copy this file”. Trong SSH1, SSH2 và OpenSSH, client chủ yếu là ssh và scp.
- **Session** : Một phiên kết nối giữa một client và một server. Nó bắt đầu sau khi client xác thực thành công đến một server và kết thúc khi kết nối chấm dứt. Session có thể được tương tác với nhau hoặc có thể là một chuyến riêng.

## ***Tìm hiểu các tùy chọn cơ bản của file cấu hình SSH***

 
### ***1. Khởi tạo phiên SSH***
- Nếu đang sử dụng Linux hoặc Mac OS , kết nối SSH khá đơn giản bằng cách sử dụng Terminal . Nếu sử dụng Windows , cần thêm 1 chương trình khác để mở kết nối SSH . Trình kết nối SSH được sử dụng phổ biến nhất cho Windows là PuTTY .
- Với Mac OS và Linux , mở Terminal và gõ lệnh theo cấu trúc sau :
    ```
    # ssh user@[host/IP]
    ```

- Trong đó :
    - `user` : user local trên máy cần ssh
    - `host/IP` : hostname ( VD : `www.xyzdomain.com` ) hoặc IP của máy cần kết nối SSH ( VD : `244.235.23.19` )

- Sau khi thực hiện lệnh , máy đầu xa sẽ yêu cầu password của user sử dụng SSH .

### ***2. File cấu hình SSH***
#### ***Các file cấu hình ssh cần lưu ý:***
- `/etc/ssh/sshd_config` : file cấu hình SSH Server
- `/etc/ssh/ssh_config` : file cấu hình SHS Client
- `~/.ssh/` : thư mục chứa nội dung cấu hình SSH của user client trên Linux
- `/etc/nologin` : Nếu file này tồn tại, thì dịch vụ SSH Server trên Linux sẽ từ chối đăng nhập từ các user khác trên hệ thống trừ user `root`. File này thường dùng cho trường hợp khẩn cấp cần cách ly hệ thống sớm

#### ***Chỉnh sửa file cấu hình SSH***
Để chỉnh sửa file cấu hình ssh, ta sử dụng lệnh sau
```
vi /etc/ssh/sshd_config
:set nu
```

![IMG](./IMG/1.png)

##### ***1. Đổi port SSH***
- Dịch vụ SSH mặc định hoạt động trên port `22` . Vì là port phổ biến , rất dễ bị kẻ xấu thực hiện các hoạt động dò tìm mật khẩu tự động đăng nhập SSH vào hệ thống .

- Để điều chỉnh port mặc định , xuống dòng `17 Port`, chỉ định port mới , đồng thời bỏ dấu `#` ở đầu dòng. Ví dụ, ta đổi sang `port 6666`

    ![IMG](./IMG/2.png)

##### ***2. Giới hạn IP lắng nghe ssh***
- Nếu hệ thống có nhiều hơn 1 địa chỉ IP thì tốt nhất nên chỉ định rõ địa chỉ IP nào sẽ lắng nghe port SSH . Thực hiện sửa đổi ở dòng `19 ListenAddress` , đồng thời bỏ dấu `#` ở đầu dòng ( `0.0.0.0` có nghĩa là mọi IP đều lắng nghe SSH ):

     ![IMG](./IMG/3.png)

##### ***3. Timeout khi user đăng nhập không thành công***
- Khi 1 user đăng nhập SSH , nếu không chỉ định thông tin user từ đầu thì sẽ hiện ra 1 prompt yêu cầu nhập thông tin user . Sau đó là phần nhập mật khẩu nếu user đó đăng nhập bằng mật khẩu . Ta sẽ quy định thời gian 1 kết nối SSH đợi cho hoạt động đăng nhập user thành công , nếu sau khoảng thời gian này không đăng nhập được thì ngắt kết nối. 

- Thay đổi tùy chọn này ở dòng `37 LoginGraceTime`( mặc định đã được cấu hình là 2 phút )

   ![IMG](./IMG/4.png)

##### ***4. Không cho user `root` đăng nhập***
- Để tăng tính bảo mật cho hệ thống, bạn không nên cho đăng nhập bằng user `root`.

- Khi muốn sử dụng quyền `root` thì chỉ cần tạo user rồi cấp quyền sudo cho user đó.

- Để ngăn không cho ssh bằng tài khoản `root`. Tìm đến dòng `38 PermitRootLogin`, sửa `yes` thành `no` đồng thời bỏ dấu `#` ở đầu dòng :

    ![IMG](./IMG/5.png)

##### ***5. Chế độ "Strict Mode"***
- Ta sẽ chỉ định dịch vụ SSH phải kiểm tra thông tin quyền của thư mục `$HomeUser` , thư mục `.ssh` và file `authorized_keys` chứa key SSH nếu dùng SSH key.

- Nếu không sử dụng chế độ này ( `no` ) thì SSH sẽ không kiểm tra cấu hình các quyền khi đăng nhập vào Server -> Ép người quản trị phải cấu hình đúng các phân quyền ( *permissions* ) cho các thư mục `/ key` dùng để đăng nhập SSH

- Thay đổi tùy chọn này ở dòng `39 StrictModes` (mặc định để `yes`)

  ![IMG](./IMG/6.png)

##### ***6. Thiết lập số lần đăng nhập sai tối đa***
- Nếu đăng nhập sai số lần quy định sẽ ngắt kết nối của Client .

- Thay đổi tùy chọn này ở dòng `40 MaxAuthTries`( mặc định là 6 ) :

   ![IMG](./IMG/7.png)

##### ***7. Số phiên đăng nhập SSH tối đa***
- Thay đổi giá trị tại dòng `41 MaxSessions` (mặc định là 10)

    ![IMG](./IMG/8.png)

##### ***8. Sử dụng chứng thực bằng SSH key , thay vì mật khẩu***
- Mặc định , mỗi VPS/Cloud Server sẽ đăng nhập vào bằng user root hoặc user thường . Tuy nhiên việc sử dụng mật khẩu có 2 nguy cơ lớn là :
    - Mất toàn bộ hệ thống nếu để lộ mật khẩu
    - Hacker có thể dùng phương thức tấn công **BruteForce** để dò ra mật khẩu

- Vì vậy nên dùng SSH Key để đăng nhập vào Server cũng như sử dụng nó để xác thực các kết nối từ bên ngoài vào cho an toàn hơn . Đồng thời , nếu có thể nên tắt cấu hình chứng thực mật khẩu.

- Thực hiện thay đổi ở dòng `43 PubkeyAuthentication` và `65 PasswordAuthentication`

     ![IMG](./IMG/9.png)

    ![IMG](./IMG/10.png)

##### ***9. Tắt log Last login***
- Để tắt log đăng nhập lần cuối, ta chỉnh sửa dòng `106 PrintLastLog` (mặc định là `yes`) đổi thành `no`

    ![IMG](./IMG/11.png)

##### ***10. Cấu hình thời gian ngắt kết nối SSH khi user không hoạt động***
- Có thể quy định thời gian timeout mà 1 kết nối SSH đến Server Linux không nhận được bất kỳ hoạt động tương tác nào trên Terminal SSH . Lúc này nếu quá thời gian quy định thì SSH Server sẽ tự ngắt kết nối từ các user không tương tác.

- Thực hiện thay đổi ở dòng `112 ClientAliveInterval` và `113 ClientAliveCountMax`, đồng thời bỏ dấu `#` ở đầu dòng :

   ![IMG](./IMG/12.png)

##### ***11. Giới hạn User/Group sử dụng cho SSH***
- Mặc định SSH Server cho phép tất cả các user local đăng nhập qua SSH . Nhưng đôi khi cần chặn không cho đăng nhập với 1 số user nhất định hoặc 1 nhóm cụ thể

- Để **cho phép** user hoặc group được đăng nhập SSH , thực hiện thêm vào 1 số dòng sau vào cuối file:
    ```
    AllowUsers user_name1 user_name2
    AllowGroups group_name1 group_name2
    ```

- Để **không cho phép** user hoặc group được đăng nhập SSH , thực hiện thêm vào 1 số dòng sau vào cuối file
    ```
    DenyUsers user_name1 user_name2
    DenyGroups group_name1 group_name2
    ```

##### ***12. Đường dẫn tới file key
- Nếu bạn tạo file key ở 1 vị trí khác mặc định, ta có thể thay đổi đường dẫn tại dòng `47 AuthorizedKeysFile`

    ![IMG](./IMG/13.png)

### ***3. Kiểm tra file cấu hình***
Thực hiện kiểm tra lại quá trình sửa đổi file `sshd_config` xem có sai không , nếu sai sẽ báo lỗi :
```
sshd -t
```

### ***4. Cho phép SSH qua Firewall***
```
firewall-cmd --permanent --zone=public --add-port=22/tcp
firewall-cmd --reload
```

hoặc

```
firewall-cmd --permanent --zone=public --add-service=ssh
firewall-cmd --reload
```

### ***5. Khởi động lại dịch vụ SSH***
```
systemctl restart sshd
systemctl enable sshd
```

## ***Tìm hiểu về SSH keypair***
### ***Khái niệm***
Đôi khi việc sử dụng password để đăng nhập rất là phức tạp và tiềm ẩn khả năng bị tấn công cao. Vì vậy, bạn có thể thực hiện việc kết nối thông qua sử dụng cơ chế key pair.
Cơ bản thì ở máy server 1 sẽ tiến hành tạo cặp key là private key và public key. Sau đó máy 1 sẽ gửi key public tới máy 2 và giữ lại private key. Khi muốn thực hiện đăng nhập từ xa, máy 1 sẽ gửi yêu cầu kèm key private tới máy 2. Máy 2 sẽ tiến hành kiểm tra Private key có trùng với Public Key không. Nếu có thì sẽ đăng nhập thành công.

### ***Lab SSH keypair***
1. Đầu tiên, bạn phải tiến hành tạo SSH key trên máy `ssh-keygen`
2. Lập tức trên terminal xuất hiện một số yêu cầu sau:`Enter file in which to save the key (/root/.ssh/id_rsa): `
3. Bạn sẽ điền tên của file key. Thư mục lưu trữ file key đó là thư mục `/root/.ssh/`. Nếu bạn không nhập bất cứ gì, tên file sẽ mặc định là id_rsa.

4. Tiếp theo là mật khẩu cho key. Bước này sẽ khiến bạn phải xác thực lại key bằng mật khẩu.Nếu không muốn nhập mật khẩu, nhấn Enter để bỏ qua.
```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
```


## ***Logs SSH***
### ***Khái niệm***
SSH logs là các bản ghi (logs) liên quan đến các kết nối SSH (Secure Shell) đã được thiết lập trên một hệ thống. Các bản ghi này có thể hữu ích để khắc phục sự cố liên quan đến các kết nối SSH, giám sát hoạt động hệ thống và kiểm tra hoạt động của người dùng.

### ***Các file logs phổ biến***
- Secure log: Trên hầu hết các hệ thống giống Unix, các kết nối SSH được lưu vào tệp log hệ thống tại /var/log/secure hoặc /var/log/auth.log. Tệp log này chứa một bản ghi về tất cả các yêu cầu đăng nhập SSH thành công và thất bại, bao gồm ngày và giờ của yêu cầu, tên người dùng được sử dụng để kết nối, địa chỉ IP của máy khách và các chi tiết khác.

- OpenSSH log: OpenSSH là một triển khai SSH phổ biến được sử dụng trên các hệ thống giống Unix, và nó ghi lại các kết nối SSH vào tệp được đặt tại /var/log/secure theo mặc định. Tuy nhiên, OpenSSH cũng có thể được cấu hình để ghi lại vào một tệp khác sử dụng chỉ thị LogLevel trong tệp sshd_config.

- Windows Event Log: Trên các hệ thống Windows, các kết nối SSH có thể được ghi lại vào Trình quản lý Sự kiện bằng cách sử dụng Windows Event Log. Tệp log cụ thể được sử dụng sẽ phụ thuộc vào triển khai SSH được sử dụng.

### ***Lọc logs của ssh***
`cat /var/log/auth.log |grep sshd`
 ![IMG](./IMG/14.png)

 ### ***Lọc logs SSH đăng nhập thất bại***
 `cat /var/log/auth.log | grep sshd | grep Failed`
  ![IMG](./IMG/15.png)

  