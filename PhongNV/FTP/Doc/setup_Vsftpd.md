# ***Cài đặt máy chủ FTP trên CentOS 7***
## ***1: Cài đặt dịch vụ FTP với VSFTPD***
### ***Cài đặt phần mềm VSFTPD bằng lệnh sau:***
`sudo yum install vsftpd`

![ima](../IMG/6.png)

### ***Bắt đầu dịch vụ và thiết lập để khởi chạy khi hệ thống khởi động với các thao tác sau:***
`sudo systemctl start vsftpd`
`sudo systemctl enable vsftpd`

![ima](../IMG/7.png)

### ***Tạo quy tắc cho tường lửa của bạn để cho phép lưu lượng FTP trên Cổng 21:***
```
sudo firewall-cmd --zone=public --permanent --add-port=21/tcp

sudo firewall-cmd --zone=public --permanent --add-service=ftp

sudo firewall-cmd –-reload
```

![ima](../IMG/8.png)

### ***Kiểm tra trạng thái dịch vụ:***
`systemctl status vsftpd`
![ima](../IMG/9.png)
## ***2: Cấu hình VSFTPD***
### ***2.1. Trước khi bắt đầu, hãy tạo một bản sao của tệp cấu hình mặc định:***
`sudo cp /etc/vsftpd/vsftpd.conf /etc/vsftpd/vsftpd.conf.default`

![ima](../IMG/10.png)

Điều này đảm bảo rằng bạn có cách quay lại cấu hình mặc định, trong trường hợp bạn thay đổi cài đặt có thể gây ra sự cố.

### ***2.2 Chỉnh sửa tệp cấu hình bằng lệnh sau:***
`vi /etc/vsftpd/vsftpd.conf`

![ima](../IMG/1.png)

#### ***Đặt máy chủ FTP của bạn để tắt người dùng ẩn danh và cho phép người dùng cục bộ.***

![ima](../IMG/2.png)
![ima](../IMG/3.png)
```
anonymous_enable=NO // Không cho kết nối nặc danh 
local_enable=YES        // Cho phép kết nối cục bộ
```
#### ***Cho phép người dùng đã đăng nhập tải tệp lên máy chủ FTP của bạn.***
![ima](../IMG/4.png)

#### ***Giới hạn người dùng FTP trong thư mục chính của họ***
![ima](../IMG/5.png)

- Chroot cho tất cả User:
```
chroot_local_user=YES
chroot_list_enable=NO
```
- Chroot đối với 1 số User trong danh sách được tạo trong file `/etc/vsftpd.chroot_list`
```
chroot_local_user=NO
chroot_list_enable=YES
```
- Chroot tất cả User ngoại trừ các User có trong file `/etc/vsftpd.chroot_list`
```
chroot_local_user=YES
chroot_list_enable=YES
```

Tiện ích vsftpd cung cấp cách tạo danh sách người dùng được phê duyệt.Giới hạn User đăng nhập vào hệ thống: Để chỉ cho phép một số User nhất định đăng nhập vào máy chủ FTP. Để quản lý người dùng theo cách này,thêm 2 dòng sau vào sau dòng `userlist_enable=YES`. Khi đó, những user có trong `/etc/vsftpd/user_list` mới được truy cập vào hệ thống.
```
userlist_enable=YES

userlist_file=/etc/vsftpd/user_list

userlist_deny=NO
```

### ***2.3 Sau khi chỉnh sửa xong tệp cấu hình, hãy lưu các thay đổi. Khởi động lại dịch vụ vsftpd để áp dụng các thay đổi:***
 `systemctl restart vsftpd`
 
### ***2.4 Cho phép các cổng FTP đi qua tường lửa***
```
firewall-cmd --permanent --add-port=30000-31000/tcp
success
firewall-cmd --reload
success
```
![ima](../IMG/13.png)

## ***3: Tạo một người dùng FTP mới***
```
sudo adduser phongnv
sudo passwd phongnv
```
![ima](../IMG/14.png)
### ***Thêm user vào danh sách được truy cập FTP server tại `/etc/vsftpd/user_list`***

```
echo "phongnv" | tee -a /etc/vsftpd/user_list
```

### ***Tạo thư mục cho người dùng mới và điều chỉnh quyền:***
```
mkdir -p /home/phongnv/ftp/upload
chmod 550 /home/phongnv/ftp
chmod 750 /home/phongnv/ftp/upload
chown -R phongnv: /home/phongnv/ftp
```
![ima](../IMG/18.png)


## ***Truy cập FTP Server***
- Cài đặt gói lftp:
`yum install lftp`
![ima](../IMG/19.png)
- Truy cập vào FTP Server:

`lftp ftp://phongnv@192.168.3.72`
![ima](../IMG/20.png)
hoặc
`lftp -u phongnv 192.168.3.72`

![ima](../IMG/21.png)


## ***Trên Window***
![ima](../IMG/22.png)


# ***Tài liệu tham khảo***

<https://phoenixnap.com/kb/how-to-setup-ftp-server-install-vsftpd-centos-7>

<https://github.com/danghai1996/thuctapsinh/blob/master/HaiDD/FTP/docs/1-FTP.md>








