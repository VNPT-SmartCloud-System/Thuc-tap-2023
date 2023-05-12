# Hướng dẫn cài đặt Ubuntu Server 20.04

Ubuntu Server 20.04 LTS (hỗ trợ dài hạn) được Canonical hỗ trợ đến năm 2025. Tuy nhiên có thể gia hạn các bản cập nhật bảo mật thêm 5 năm thông qua dịch vụ ESM (Extended Security Maintenance) như một phần đăng ký UA-I (Ubuntu Advantage for Infrastructure)

## 1. Những điểm mới trong Ubuntu Server 20.04 LTS

- Hỗ trợ 10 năm 
- Ubuntu Server Live Installer – cập nhật tự động
- Hỗ trợ cho tất cả các kiến ​​trúc chính: x64-64, ARM v7, ARM64, POWER 8, POWER 9, IBM s390x (LinuxONE) và giới thiệu hỗ trợ ban đầu cho RISC-V
- Cập nhật cho các ứng dụng khác nhau: QEMU (v4.2), libvirt (v6.0), PHP (v7.4), Ruby (v2.7), GCC (v9.3), Python (v3.8), MySQL (v8) .0) và NGINX (v1.17).
- Dựa trên nhân Linux dài hạn mới – 5.4 – để nhận các bản cập nhật bảo mật và hỗ trợ phần cứng mới nhất.
- Hỗ trợ cho phiên bản mới nhất của IMDS (dịch vụ siêu dữ liệu phiên bản) – IMDSv2 – trên AWS.
- Cải thiện hỗ trợ cho IPv6 trên Microsoft Azure.

## 2. Chuẩn bị

Trước tiên bạn càn truy cập vào trang chủ Ubuntu để tải về file ISO cài đặt phù hợp với hệ thống của mình. Bạn có thể bấm trực tiếp vào link sau: 

[Download Ubuntu Server 20.04 LTS](https://releases.ubuntu.com/20.04/)

## 3. Các bước cài đặt

Tạo máy ảo trên môi trường

### 3.1 Chọn ngôn ngữ

![](../img/u1.png)

### 3.2. Chọn Keyboard

Nhấn chọn **Contine without updating**

![](../img/u2.png)

Nhấn chọn **Keyboard** -> **Done**

![](../img/u3.png)

### 3.3. Cấu hình card mạng

Bước tiếp theo là cấu hình card mạng (Network Connections). Nếu máy bạn có nhiều card mạng thì cấu hình IP vào đúng tên card mạng. Trên ví dụ chỉ có duy nhất 1 card mạng, bạn bấm **Enter** hoặc ****Space** để ra Menu như hình và chọn **Edit IPv4**

![](../img/u4.png)

Bước này, nếu bạn dùng **DHCP** thì chọn **Automatic (DHCP)** để tự cấp IP, nếu bạn dùng IP tĩnh thì các bạn chuyển từ ục **Automatic (DHCP)**  sang **Manual** và khai báo IP, Subnet, Gateway, DNS như hình dưới. Sau đó nhấn **Save**.

Nhấn **Done**

### 3.4 Cấu hình Proxy

Bạn cần nhập URL và số cổng của proxy nếu bạn đang sử dụng máy chủ proxy hoặc máy chủ bộ đệm apt proxy. Nếu bạn không sử dụng proxy, bạn có thể để trống phần Proxy address. Sau đó nhấn **Done**

![](../img/u5.png)

### 3.5 Cấu hình mirror lưu trữ

Bước này hệ thống sẽ định vị được và chọn cho bạn một mirror gần nhất, có tốc độ mạng nhanh nhất để dễ dàng update phần mềm sau này

![](../img/u6.png)

**Lưu ý**: Chỉ sau khi cấu hình IP ra mạng Internet được mới có thể định vị được

### 3.6. Phân vùng đĩa cài đặt OS

Nếu muốn nhanh chóng, các bạn chỉ cần chọn **Use an




