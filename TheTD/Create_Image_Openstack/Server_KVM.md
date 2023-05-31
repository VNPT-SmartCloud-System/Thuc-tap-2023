# **Chuẩn bị Server KVM**

Kiểm tra `vmx enable` trên **KVM host**

    cat /proc/cpuinfo| egrep -c "vmx|svm"

>*Sẽ đếm số lượng CPU hỗ trợ các tính năng ảo hóa Intel (vmx) hoặc AMD (svm)*

>*Nếu đầu ra là "0", điều đó có nghĩa là CPU không hỗ trợ tính năng ảo hóa*

Install epel-release và update 
```sh 
yum install epel-release -y && yum update -y 
```

Cài đặt KVM Node để đóng Images
```
yum install -y qemu-kvm qemu-img virt-manager libvirt libvirt-python libvirt-client \
virt-install virt-viewer bridge-utils  "@X Window System" xorg-x11-xauth xorg-x11-fonts-* \
xorg-x11-utils mesa-libGLU*.i686 mesa-libGLU*.x86_64 dejavu-lgc-sans-fonts
touch /root/.Xauthority
```



Kiểm tra xem `libvirtd` đã được khởi động chưa
```sh
systemctl status libvirtd
```
Nếu `libvirtd` chưa được khởi động, hãy chạy lệnh sau
```sh 
systemctl start --now libvirtd
```

Disable ipv6 (Hiện nay không cần disable nữa)
```sh
echo "net.ipv6.conf.all.disable_ipv6 = 1" >> /etc/sysctl.conf
echo "net.ipv6.conf.default.disable_ipv6 = 1" >> /etc/sysctl.conf
sysctl -p
```

Enable `X11Forwarding yes` trong `/etc/ssh/sshd_config` 

**X11 forwarding** là một tính năng trong SSH cho phép chạy các ứng dụng đồ họa trên máy chủ từ xa và hiển thị chúng trên máy tính của bạn thông qua giao thức X11. Khi **X11 forwarding** được bật, bạn có thể chạy các ứng dụng đồ họa trên máy chủ CentOS và hiển thị chúng trên máy tính của bạn thông qua SSH
```sh
X11Forwarding yes
```

Thêm cấu hình `/etc/ssh/sshd_config` để sử dụng X11Forward khi disable IPv6
```sh
X11Forwarding yes
AddressFamily inet
```

Restart SSH
```sh
systemctl restart sshd
```

Tạo folder channel cho các target của VM: Thư mục channel được sử dụng để truyền thông giữa các máy ảo và host.
```
mkdir -p /var/lib/libvirt/qemu/channel/target
chown -R qemu:kvm /var/lib/libvirt/qemu/channel
```

Restart libvirt 
```sh
systemctl restart libvirtd
```

Cài libguestfs-tools để xử lý file `.qcow2` thành file `.img` sau khi cài đặt cấu hình xong VM.
```sh
yum install libguestfs-tools -y
```

Bật tính năng `nestes` cho phép ảo hóa trên VM 
```sh 
touch /etc/modprobe.d/kvm.conf
echo "options kvm_intel nested=1" > /etc/modprobe.d/kvm.conf
init 6
```

Copy Images vào VM => Tiến hành đóng Images
Enable `X11Forwarding` trong `etc/ssh/sshd_confgig`

# Tài liệu tham khảo
[Đặng Xuân Cảnh, Jan - 2 - 2020, KVM_Install, Apr - 7 - 2023](https://github.com/nhanhoadocs/create-images-openstack/blob/master/docs/KVM_install.md)
