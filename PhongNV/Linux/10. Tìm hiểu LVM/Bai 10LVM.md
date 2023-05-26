# ***Khái niệm***
Logical Volume Management(LVM) dùng quản lí các thiết bị lưu trữ .LVM là một tiện ích cho phép chia không gian đĩa cứng thành những Logical Volume từ đó giúp cho việc thay đổi kích thước trở nên dễ dàng.
# ***Tại sao cần phải sử dụng LVM***
-	Quản lý dung lượng dễ dàng: LVM cho phép quản lý dung lượng một cách linh hoạt và dễ dàng hơn.
-	Tính linh hoạt cao: LVM cho phép chia sẻ dữ liệu giữa nhiều hệ thống hoặc cung cấp bảo vệ dữ liệu bằng cách sao lưu dữ liệu sang các ổ đĩa khác.
-	Bảo mật dữ liệu: LVM cung cấp tính năng snapshot, cho phép tạo ra các bản sao của các phân vùng, giúp bảo vệ dữ liệu trước các sự cố như lỗi phần cứng hoặc virus.
-	Tối ưu hóa hiệu suất: LVM cho phép tối ưu hóa hiệu suất bằng cách tạo ra các phân vùng ở các vị trí vật lý khác nhau trên nhiều ổ đĩa, giúp tăng tốc độ truy xuất dữ liệu. 
-	Dễ dàng quản lý: LVM cung cấp các công cụ quản lý dễ sử dụng để tạo, xóa hoặc tăng kích thước các phân vùng.
# ***Thành phần trong LVM***
## ***Physical Volumes(PV)***
-	Đĩa cứng vật lý trong server
-	Có thể kết hợp nhiều PV để tạo thành một Volume Group 
-	PV chỉ là đại diện cho các ổ đĩa vật lý chứ không phải là bản thân ổ đĩa đó, vì vậy để cần phải tạo PV từ cá dev đã mount.
## ***Volume Groups(VG)***
-	Một tập hợp các PV từ VG có thể phân chia thành các Logical Volumes và các Logical Volumes này có thể thay đổi kích thước dễ dàng.
## ***Logical Volume(LV)***
-	Đơn vị cuối cùng của hệ thống LVM, các LV tương đương với partition theo cách phân chia truyền thống.
-	LV có thể thay đổi kích thước dễ dàng, tất cả chỉ phụ thuộc vào kích thước của VG.
# ***Tạo và quản lý LVM***
-	Tạo Physical Volume
```
# pvcreate /dev/sdb1
  Physical volume "/dev/sdb1" successfully created
# pvs
  PV         VG   Fmt  Attr PSize   PFree
  /dev/sdb1       lvm2 ---  232.88g 232.88g
# pvscan
  PV
  /dev/sdb1           lvm2 [232.88 GiB]
  Total: 3 [465.28 GiB] / in use: 2 [232.39 GiB] / in no VG: 1 [232.88 GiB]
# pvdisplay
 "/dev/sdb1" is a new physical volume of "232.88 GiB"
  --- NEW Physical volume ---
  PV Name               /dev/sdb1
  VG Name
  PV Size               232.88 GiB
  Allocatable           NO
  PE Size               0
  Total PE              0
  Free PE               0
  Allocated PE          0
PV UUID               ajGCMg-Y4cG-v4AD-Wxma-TaE5-zQig-XmnYAx
```
-	Tạo Volume Group
```
# vgcreate storage /dev/sdb1
  Volume group "storage" successfully created
# vgscan
  Reading all physical volumes.  This may take a while...
  Found volume group "storage" using metadata type lvm2
# vgs
  VG      #PV #LV #SN Attr   VSize   VFree
  storage   1   0   0 wz--n- 232.88g 232.88g
# vgdisplay
  --- Volume group ---
  VG Name               storage
  System ID
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               232.88 GiB
  PE Size               4.00 MiB
  Total PE              59618
  Alloc PE / Size       0 / 0
  Free  PE / Size       59618 / 232.88 GiB
VG UUID               nEcTxG-p5K6-npqD-OVeX-dRI1-aWP9-o4D1Z1
```
-	Tạo Logical volume
```
# lvcreate -L 20G -n db-area storage
  Logical volume "db-area" created.
# lvcreate -L 10G -n users-area storage
  Logical volume "users-area" created.
# lvcreate -L 60G -n staging-area storage
  Logical volume "staging-area" created.
# lvcreate -l 100%FREE -n spare storage
  Logical volume "spare" created.
# lvs
  LV           VG      Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  db-area      storage -wi-a-----  20.00g
  spare        storage -wi-a----- 142.88g
  staging-area storage -wi-a-----  60.00g
  users-area   storage -wi-a-----  10.00g
# lvscan
  ACTIVE            '/dev/storage/db-area' [20.00 GiB] inherit
  ACTIVE            '/dev/storage/users-area' [10.00 GiB] inherit
ACTIVE            '/dev/storage/staging-area' [60.00 GiB] inherit
```
-	Tạo nơi lưu trữ 
```
# mkfs.ext4 /dev/storage/db-area
# mkfs.ext4 /dev/storage/users-area
# mkfs.ext4 /dev/storage/staging-area
# mkfs.ext4 /dev/storage/spare

# mkdir /db
# mount /dev/storage/db-area /db
# mkdir /users
# mount /dev/storage/users-area /users
# mkdir /staging
# mount /dev/storage/staging-area /staging
```


# ***Tìm hiểu lệnh `mkfs`***
 Là tạo các hệ thống tệp. Hay gọi khác có thể 
được gọi là định dạng.Đó là quá trình chuẩn bị 
một phân vùng để nó có thể lưu trữ dữ liệu. Phân 
vùng cần một cách để lưu tập tin, vâng.

 - Hệ thống tệp có sẵn

```
  $ mkfs
mkfs         mkfs.cramfs  mkfs.ext3    mkfs.
fat     mkfs.msdos   mkfs.vfat
mkfs.bfs     mkfs.ext2    mkfs.ext4    mkfs.
minix   mkfs.ntfs    
```


Các thư mục trên đề cập đến các lệnh `mkfs` để 
tạo ra các loại hệ thống tập tin khác nhau trên 
Linux.

- `mkfs.bfs`: tạo ra một hệ thống tập tin BFS 
(BeOS File System).
- `mkfs.cramfs`: tạo ra một hệ thống tập tin 
CRAMFS (Compressed ROM File System), được sử dụng 
cho các thiết bị nhúng.
- `mkfs.ext2`, `mkfs.ext3`, `mkfs.ext4`: tạo ra 
các hệ thống tập tin ext2, ext3 và ext4, được sử 
dụng phổ biến trên các bản phân phối Linux.
- `mkfs.fat`, `mkfs.msdos`, `mkfs.vfat`: tạo ra 
các hệ thống tập tin FAT (File Allocation Table), 
MS-DOS và VFAT, được sử dụng trên các thiết bị 
lưu trữ di động như USB hoặc thẻ nhớ.
- `mkfs.minix`: tạo ra một hệ thống tập tin 
Minix, được sử dụng trên một số bản phân phối 
Linux và các thiết bị nhúng.

Các lệnh `mkfs` này được sử dụng để tạo ra các hệ 
thống tập tin trên các thiết bị lưu trữ khác 
nhau, tùy thuộc vào mục đích sử dụng và yêu cầu 
của người dùng.

# ***Tìm hiểu lệnh `mount`***
Lệnh `mount` trong Linux được sử dụng để kết nối 
một hệ thống tập tin đã được tạo trên một thiết 
bị lưu trữ (như ổ đĩa cứng, USB, thẻ nhớ, ...) 
vào một thư mục trên hệ thống tập tin hiện tại. 
Kết nối hệ thống tập tin này có thể cho phép bạn 
truy cập và sử dụng các tập tin và thư mục được 
lưu trữ trên thiết bị đó.

# ***Lệnh `lvscan` trong linux***
Trong LVM (Logical Volume Manager) trên Linux, 
lệnh `lvscan` được sử dụng để quét các Logical 
Volume (LV) hiện có và hiển thị thông tin về 
chúng.

Cú pháp của lệnh `lvscan` như sau:

```
lvscan [options]
```

Trong đó, `options` là các tùy chọn để cấu hình 
lệnh. Một số tùy chọn phổ biến của `lvscan` như 
sau:

- `-a`: Quét tất cả các Volume Group (VG) và LV, 
bao gồm cả những LV đang bị khóa.
- `-c`: Hiển thị kết quả dưới dạng cột.
- `-d`: Hiển thị kết quả dưới dạng giảm dần 
(descending).
- `-h`: Hiển thị kết quả dưới dạng đơn vị được 
định dạng (megabytes, gigabytes, ...).
- `-o`: Chỉ định các trường thông tin để hiển 
thị, ví dụ như `lv_name`, `lv_size`, `vg_name`, 
`lv_path`, `lv_attr`, ...

Khi được chạy, `lvscan` sẽ quét các LV hiện có 
trên hệ thống và hiển thị thông tin về chúng, bao 
gồm tên LV, dung lượng, VG chứa LV, đường dẫn đến 
LV, trạng thái của LV, ...

# ***Tạo 2 phân vùng***
```
$ fdisk /dev/sdb

Welcome to fdisk (util-linux 2.37.2).
Changes will remain in memory only, until you 
decide to write them.
Be careful before using the write command.

fdisk: cannot open /dev/sdb: No such file or 
directory
vanphong17@vanphong17-Inspiron-5490:~$ pvcreate /
dev/sdb
  WARNING: Running as a non-root user. 
Functionality may be unavailable.
  /run/lock/lvm/P_global:aux: open failed: 
Permission denied
vanphong17@vanphong17-Inspiron-5490:~$ sudo -i
[sudo] password for vanphong17: 
root@vanphong17-Inspiron-5490:~# pvcreate /dev/sdb
  No device found for /dev/sdb.
root@vanphong17-Inspiron-5490:~# pvcreate /dev/
sdb1
  No device found for /dev/sdb1.
root@vanphong17-Inspiron-5490:~# su - vanphong17
vanphong17@vanphong17-Inspiron-5490:~$ pvcreate /
dev/sdb1
  WARNING: Running as a non-root user. 
Functionality may be unavailable.
  /run/lock/lvm/P_global:aux: open failed: 
Permission denied
```






# ***Tài liệu tham khảo***
https://viblo.asia/p/linux-tim-hieu-lvm-trong-linux-Az45b0woZxY
https://itzone.com.vn/vi/article/tim-hieu-lvm-trong-linux/

