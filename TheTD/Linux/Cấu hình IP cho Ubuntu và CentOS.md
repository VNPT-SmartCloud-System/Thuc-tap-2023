# Hướng dẫn cấu hình địa chỉ IP cho Ubuntu và CentOS

# Ubuntu

Kể từ phiên bản 18.04 trở đi, việc cấu hình mặc định trong Ubuntu sẽ sử dụng netplan thay vì cách sửa file như cũ.

## Cấu hình IP cho ubuntu sử dụng file /etc/netplan/01-network-manager-all.yaml

Hiển thị nọi dung của file bằng lệnh `cat`

```sh
cloud@cloud:~$ cat /etc/netplan/01-network-manager-all.yaml
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.126.143/24]
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```
Sửa file `/etc/netplan/ .yaml bằng 2 cách
- Dùng các công cụ chỉnh sửa như nano, vi, vim,...
- Dùng lệnh `echo` để chèn nội dung file 

### **Cách 1: Dùng công cụ chỉnh sửa**

Sử dụng **vim** để mở file:
```sh
vi  /etc/netplan/01-network-manager-all.yaml
```
Nội dung bên trong
```sh
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      dhcp4: no
      addresses: [192.168.126.143/24]
      gateway4: 192.168.126.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```
Có thể chỉnh sửa các thông số của một giao diện mạng như sau
- Địa chỉ ip: sử dụng khai báo `addresses` với cú pháp CIDR (192.168.126.143/24) và chỉ định giao thức mạng (**dhcp** hoặc **static**)
- Subnet mask: như trên
- Gateway: sử dụng khai báo `gateway4` với địa chỉ ip của gateway
- DNS: sử dụng khai báo `namesevers` với danh sách địa chỉ IP của DNS servers 
- Các giao thức mạng: sử dụng khai báo `dhcp4` hoặc `dhcp6` để sử dụng DHCP hoặc `addresses` để cấu hình địa chỉ IP tĩnh

Sau khi chỉnh sửa file xong, chạy lệnh `sudo netplan apply` để áp dụng thay đổi

### **Cách 2: Sử dụng lệnh echo để chèn nội dung file**

Để chèn nội dung vào tệp cấu hình Netplan bằng lệnh `echo`, bạn có thể sử dụng cú pháp sau:

```sh
echo "Nội dung" | sudo tee /etc/netplan/ten-tap-tin.yaml
```

Trong đó:

- `Nội dung`: là nội dung muốn chèn vào tệp cấu hình.
- `/etc/netplan/ten-tap-tin.yaml`: là đường dẫn và tên của tệp cấu hình muốn chèn nội dung vào.

Ví dụ: để chèn cấu hình mạng với địa chỉ IP tĩnh 192.168.1.100 và gateway 192.168.1.1 vào tệp cấu hình /etc/netplan/01-netcfg.yaml, bạn có thể sử dụng lệnh sau:

```sh
echo "network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.1.100/24]
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]" | sudo tee /etc/netplan/01-netcfg.yaml
```

Lưu ý rằng tệp cấu hình Netplan phải có định dạng YAML và phải tuân thủ các quy tắc định dạng YAML để được đọc bởi Netplan.

# CentOS

## ID network interfaces

Sử dụng lệnh `ip link show` hoặc `ifconfig` để liệt kê tất cả các interface hoạt động trên hệ thống

```sh
thetd ~]$ ip link show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether 00:0c:29:8a:f5:b1 brd ff:ff:ff:ff:ff:ff
```
Thông tin được hiển thị bao gồm tên giao diện, loại giao diện, trạng thái, địa chỉ MAC, MTU (Maximum Transmission Unit), và các thông số khác liên quan đến giao diện mạng.

## Chỉnh sửa file cấu hình IP tĩnh cho card mạng tương ứng
Để cấu hình IP cho CentOS bằng cách sửa file cấu hình, ta có thể làm như sau:

1. Sử dụng trình soạn thảo để mở file cấu hình network:

   ```sh
   sudo vi /etc/sysconfig/network-scripts/ifcfg-<interface-name>
   ```

   Trong đó, `<interface-name>` là tên giao diện mạng mà ta muốn cấu hình, ví dụ như `eth0` hoặc `enp0s3`.

2. Trong file cấu hình, chỉnh sửa các thông tin cần thiết như IP address, subnet mask, gateway và DNS server. Ví dụ:

   ```sh
   DEVICE=ens33
   BOOTPROTO=none
   ONBOOT=yes
   IPADDR=192.168.1.100
   NETMASK=255.255.255.0
   GATEWAY=192.168.1.1
   DNS1=8.8.8.8
   DNS2=8.8.4.4
   ```

   Trong đó, `DEVICE` là tên của giao diện mạng, `BOOTPROTO` được đặt là `none` để chỉ định rằng ta sẽ cấu hình IP tĩnh. `ONBOOT` được đặt là `yes` để bật giao diện mạng khi khởi động hệ thống. `IPADDR`, `NETMASK` và `GATEWAY` là các thông tin về IP address, subnet mask và gateway tương ứng. `DNS1` và `DNS2` là các địa chỉ DNS server.

3. Lưu và đóng file cấu hình.

4. Khởi động lại dịch vụ network để áp dụng các thay đổi:

   ```sh
   sudo systemctl restart network
   ```

## Cấu hình Network bằng nmcli 

Công cụ **nmcli "Network Manager Command-Line Interface"**. Đây là một công cụ dòng lệnh trên Linux được sử dụng để quản lý mạng thông qua Network Manager, một tiện ích quản lý mạng trên các phiên bản Linux phổ biến. nmcli cung cấp các lệnh để hiển thị, tạo và chỉnh sửa các kết nối mạng, thông tin mạng, cài đặt VPN, tạo các kết nối bridge, bond và VLAN, v.v. nmcli cũng được sử dụng để cấu hình các thông số mạng như địa chỉ IP, subnet mask, gateway và DNS

### Thêm kết nối mạng

Lệnh **nmcli con add** được sử dụng để thêm các kết nối mạng mới.
```sh
sudo nmcli connection add con-name <tên-kết-nối> ifname <tên-giao-diện-mạng> type <kiểu-kết-nối> <các-tham-số-kết-nối>
```
Trong đó:

- <tên-kết-nối>: là tên của kết nối mạng bạn muốn thêm.
- <tên-giao-diện-mạng>: là tên giao diện mạng (interface) bạn muốn sử dụng cho kết nối mạng.
- <kiểu-kết-nối>: là kiểu kết nối mạng bạn muốn thêm, ví dụ như Ethernet, Wi-Fi, VPN, v.v.
- <các-tham-số-kết-nối>: là các tham số cấu hình kết nối, ví dụ như địa chỉ IP, subnet mask, gateway, DNS, v.v.

VD: 
```sh
~]$ sudo nmcli connection add con-name MyEthernet ifname ens3 type ethernet
Connection 'MyEthernet' (72b86f3e-0c96-4dd2-be7b-94e62637f58e) successfully added.
```
Bạn cũng có thể thêm các thông số cấu hình kết nối như địa chỉ IP, subnet mask, gateway, DNS, v.v. vào lệnh trên bằng cách thêm các tham số tương ứng. Ví dụ, để thêm địa chỉ IP cho kết nối mạng này, bạn có thể sử dụng lệnh sau
```sh
sudo nmcli connection modify MyEthernet ipv4.addresses 192.168.0.2/24 ipv4.gateway 192.168.0.1 ipv4.dns 8.8.8.8
```
### Kiểm soát kết nối mạng

- Kiểm tra kết nối: `nmcli con show`
- Kích hoạt kết nối mạng: `nmcli con up <tên-kết-nối>`
- Ngắt kết nối: `nmcli dev disconnect device <tên-thiết-bị>`
- Sửa đổi cài đặt của một kết nối mạng: `nmcli con mod <tên-kết-nối> <tùy-chọn> <giá-trị>`
    vd `nmcli con mod ens33 ipv4.addresses 192.168.1.100/24 ipv4.gateway 192.168.1.1`
- Xóa kết nối mạng: `nmcli con del name <tên-kết-nối>`
- Hiển thị trạng thái: `nmcli dev status`

## Cấu hình Network bằng nmtui

**nmtui (NetworkManager Text User Interface)** nhằm cung cấp cho chúng ta một giao diện text cấu hình linh động tương tác với NetworkManager ngay trên Terminal hoặc Console kết nối đến hệ thống thay vì phải dùng lệnh riêng của Network Manager

```sh
nmtui edit <tên-kết-nối>
```
![](../Linux/img/nmtui.png)

