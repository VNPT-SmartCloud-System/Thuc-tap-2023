## ***Logs SSH***
### ***Khái niệm***
SSH logs là các bản ghi (logs) liên quan đến các kết nối 
SSH (Secure Shell) đã được thiết lập trên một hệ thống. 
Các bản ghi này có thể hữu ích để khắc phục sự cố liên 
quan đến các kết nối SSH, giám sát hoạt động hệ thống và 
kiểm tra hoạt động của người dùng.

### ***Các file logs phổ biến***
- Secure log: Trên hầu hết các hệ thống giống Unix, các 
kết nối SSH được lưu vào tệp log hệ thống tại /var/log/
secure hoặc /var/log/auth.log. Tệp log này chứa một bản 
ghi về tất cả các yêu cầu đăng nhập SSH thành công và 
thất bại, bao gồm ngày và giờ của yêu cầu, tên người dùng 
được sử dụng để kết nối, địa chỉ IP của máy khách và các 
chi tiết khác.

- OpenSSH log: OpenSSH là một triển khai SSH phổ biến 
được sử dụng trên các hệ thống giống Unix, và nó ghi lại 
các kết nối SSH vào tệp được đặt tại /var/log/secure theo 
mặc định. Tuy nhiên, OpenSSH cũng có thể được cấu hình để 
ghi lại vào một tệp khác sử dụng chỉ thị LogLevel trong 
tệp sshd_config.

- Windows Event Log: Trên các hệ thống Windows, các kết 
nối SSH có thể được ghi lại vào Trình quản lý Sự kiện 
bằng cách sử dụng Windows Event Log. Tệp log cụ thể được 
sử dụng sẽ phụ thuộc vào triển khai SSH được sử dụng.

### ***Lọc logs của ssh***
`cat /var/log/auth.log |grep sshd`
 ![IMG](../IMG/14.png)

 ### ***Lọc logs SSH đăng nhập thất bại***
 `cat /var/log/auth.log | grep sshd | grep Failed`
  ![IMG](../IMG/15.png)

  