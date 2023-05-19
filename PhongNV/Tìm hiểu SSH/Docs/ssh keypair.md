## ***Tìm hiểu về SSH keypair***
### ***Khái niệm***
Đôi khi việc sử dụng password để đăng nhập rất là phức 
tạp và tiềm ẩn khả năng bị tấn công cao. Vì vậy, bạn có 
thể thực hiện việc kết nối thông qua sử dụng cơ chế key 
pair.
Cơ bản thì ở máy server 1 sẽ tiến hành tạo cặp key là 
private key và public key. Sau đó máy 1 sẽ gửi key publi
tới máy 2 và giữ lại private key. Khi muốn thực hiện đăn
nhập từ xa, máy 1 sẽ gửi yêu cầu kèm key private tới máy
2. Máy 2 sẽ tiến hành kiểm tra Private key có trùng với 
Public Key không. Nếu có thì sẽ đăng nhập thành công.

### ***Lab SSH keypair***
1. Đầu tiên, bạn phải tiến hành tạo SSH key trên máy 
`ssh-keygen`
2. Lập tức trên terminal xuất hiện một số yêu cầu 
sau:`Enter file in which to save the key (/root/.ssh/
id_rsa): `
3. Bạn sẽ điền tên của file key. Thư mục lưu trữ file ke
đó là thư mục `/root/.ssh/`. Nếu bạn không nhập bất cứ 
gì, tên file sẽ mặc định là id_rsa.

4. Tiếp theo là mật khẩu cho key. Bước này sẽ khiến bạn 
phải xác thực lại key bằng mật khẩu.Nếu không muốn nhập 
mật khẩu, nhấn Enter để bỏ qua.
```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
```