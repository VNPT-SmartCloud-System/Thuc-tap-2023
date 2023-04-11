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

# ***Tài liệu tham khảo***
https://viblo.asia/p/linux-tim-hieu-lvm-trong-linux-Az45b0woZxY
https://itzone.com.vn/vi/article/tim-hieu-lvm-trong-linux/

