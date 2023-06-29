# ***Kiểm tra cài đặt `tcpdump`***
```
tcpdump -D
```
- Cài đặt gói `tcpdump`
```
yum install tcpdump
```
- Kiểm tra lại đã thấy các interface đang có sẵn để theo dõi
![ima](../IMG/22.png)

- Để bắt gói tin ta phải tắt không nhận địa chỉ IP từ DHCP Server

```
vi /etc/sysconfig/network-scripts/ifcfg-enp0s3
```
![ima](../IMG/23.png)
- Sau đó `reboot` lại.

- Bây giờ, interface enp0s3 chưa được set địa chỉ IP. Ta sẽ mở 2 terminal. 1 bên chỉnh sửa file cấu hình interface enp0s3- ta đặt BOOTPROTO = "dhcp", 1 bên 
# ***Phân tích gói tín `DHCP`***
- Giải phóng IP đã gán cho card `enp0s3`

```
dhclient -r
```
- sau đó yêu cầu cấp lại địa chỉ IP
```
dhclient -v
```
- sử dụng tcpdump để bắt gói tin khi DHCP cung cấp IP
![ima](../IMG/21.png)