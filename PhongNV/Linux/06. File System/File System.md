# ***Khái niệm***
Trong Linux, hệ thống tệp (File System) được sử dụng để quản lý và tổ chức các tệp và thư mục trên đĩa cứng hoặc bất kỳ thiết bị lưu trữ nào khác. Hệ thống tệp được thiết kế để cung cấp một phương pháp hiệu quả để lưu trữ và truy cập dữ liệu trên hệ thống Linux.

# ***Cấu trúc hệ thống tập tin***
Trên nhiều hệ thống, bao gồm cả Linux, hệ thống tệp tin được cấu trúc như một cây. Cây thường được miêu tả theo hướng ngược lại, bắt đầu từ thư mục gốc, thường được gọi là thư mục gốc, đánh dấu sự bắt đầu của hệ thống tệp tin phân cấp và cũng được biểu thị bằng /.

- Tiêu chuẩn phân cấu trúc hệ thống tệp tin (FHS) được phát triển dựa trên các tiêu chuẩn lịch sử từ các phiên bản đầu tiên của UNIX. FHS cung cấp cho các nhà phát triển Linux và quản trị hệ thống một cấu trúc thư mục tiêu chuẩn cho hệ thống tệp tin, cung cấp tính nhất quán giữa các hệ thống và bản phân phối. Linux hỗ trợ các loại hệ thống tệp tin khác nhau được tạo cho Linux, cùng với các hệ thống tệp tin tương thích từ các hệ điều hành khác. Nhiều hệ thống tệp tin cũ hơn, kế thừa được hỗ trợ. Một số ví dụ về các loại hệ thống tệp tin mà Linux hỗ trợ là:
Linux hỗ trợ nhiều loại hệ thống tệp khác nhau như Ext4, Btrfs, XFS, NTFS và FAT32. Các hệ thống tệp này khác nhau về cấu trúc, cách thức hoạt động và tính năng của chúng.

Một số hệ thống tệp phổ biến trong Linux bao gồm:

  - `Ext4`: Là hệ thống tệp mặc định cho hầu hết các bản phân phối Linux hiện đại. Nó cung cấp tính năng bảo mật tốt, hỗ trợ các tập tin lớn hơn 16 TB và cho phép tạo ra các bản sao của các tệp dự phòng.

- `Btrfs`: Là một hệ thống tệp mới được giới thiệu vào năm 2009. Nó có nhiều tính năng tiên tiến như khả năng tạo ra các tệp sao lưu tự động, tính năng tương tự như RAID và hỗ trợ cho tệp lớn hơn 16 exabytes.

- `XFS`: Là một hệ thống tệp nhanh và đáng tin cậy, được sử dụng cho các máy chủ và hệ thống lưu trữ dữ liệu lớn. Nó hỗ trợ tệp lớn và có thể chứa hàng triệu tệp.

- `NTFS`: Là hệ thống tệp của Windows và được hỗ trợ trên Linux để đọc và ghi dữ liệu trên các phân vùng NTFS.

- `FAT32`: Là hệ thống tệp cũ và không an toàn, được sử dụng để đọc và ghi dữ liệu trên các thiết bị lưu trữ nhỏ như USB hoặc thẻ nhớ.

Quản lý hệ thống tệp trên Linux có thể được thực hiện bằng cách sử dụng các lệnh như ls, mkdir, rm và cp. Ngoài ra, người dùng cũng có thể sử dụng các công cụ đồ họa như Nautilus để quản lý tệp và thư mục trên hệ thống.

- Mỗi hệ thống tệp tin đặt trên một phân vùng đĩa cứng. Phân vùng giúp tổ chức nội dung của ổ đĩa theo loại dữ liệu và cách sử dụng. Ví dụ, các chương trình quan trọng cần thiết để chạy hệ thống thường được giữ trên một phân vùng riêng biệt so với phân vùng chứa các tệp tin của người dùng thông thường. Ngoài ra, các tệp tin tạm thời được tạo và xóa trong quá trình hoạt động bình thường của Linux thường được đặt trên một phân vùng riêng; như vậy, sử dụng toàn bộ không gian có sẵn trên một phân vùng cụ thể có thể không ảnh hưởng đến hoạt động bình thường của hệ thống.
- Trước khi bạn có thể bắt đầu sử dụng hệ thống tệp tin, bạn cần phải gắn nó vào cây hệ thống tệp tin tại một điểm gắn kết (mountpoint). Điều này đơn giản là một thư mục (có thể hoặc không phải là thư mục trống) nơi hệ thống tệp tin được đính kèm (gắn kết). Đôi khi bạn có thể cần phải tạo thư mục nếu nó chưa tồn tại. Nếu bạn gắn kết hệ thống tệp tin vào một thư mục không trống, các nội dung trước đó của thư mục đó sẽ bị che khuất và không thể truy cập cho đến khi hệ thống tệp tin bị gỡ bỏ khỏi điểm gắn kết. Do đó, các điểm gắn kết thường là các thư mục trống.

# ***Thư mục người dùng***
- Trong bất kỳ hệ thống UNIX nào, mỗi người dùng đều có thư mục cá nhân của riêng mình, thường được đặt trong thư mục /home. Thư mục /root trên các hệ thống Linux hiện đại chỉ là thư mục chứa các tệp của người dùng root. Thư mục /home thường được gắn kết như một hệ thống tệp tin riêng trên một phân vùng riêng của nó, hoặc được xuất từ xa trên mạng thông qua NFS.’
- The home directory (thư mục người dùng) trong Linux là nơi lưu trữ các tệp và thư mục riêng của mỗi người dùng trên hệ thống. Mỗi người dùng có một thư mục home riêng để lưu trữ các tệp cá nhân của mình như tài liệu, ảnh, video, cài đặt ứng dụng, và các tệp cấu hình. Thư mục home được đặt tên theo tên đăng nhập của người dùng và thường nằm trong thư mục /home trên hệ thống.

Ví dụ, nếu tên đăng nhập của người dùng là "user1", thư mục home của người dùng này sẽ được đặt tại đường dẫn /home/user1 trên hệ thống. Người dùng có quyền truy cập, chỉnh sửa, tạo và xóa các tệp và thư mục trong thư mục home của họ.

Một số tệp và thư mục quan trọng trong thư mục home của mỗi người dùng bao gồm:

- `bashr`c: tệp cấu hình cho Bash shell
- `profile`: tệp cấu hình cho môi trường người dùng
- `ssh/`: thư mục lưu trữ khóa SSH của người dùng
- `Desktop/`: thư mục nơi lưu trữ các biểu tượng và tập tin trên màn hình máy tính để bàn của người dùng
- `Documents/`: thư mục nơi lưu trữ các tài liệu cá nhân của người dùng
- `Downloads/`: thư mục nơi lưu trữ các tệp tải xuống của người dùng
- `Music/`: thư mục nơi lưu trữ các tệp âm nhạc của người dùng
- `Pictures/`: thư mục nơi lưu trữ các tệp hình ảnh của người dùng
- `Public/`: thư mục nơi lưu trữ các tệp có thể chia sẻ với các người dùng khác trên cùng một hệ thống.
Thư mục home cũng có thể được chia sẻ qua mạng hoặc được định cấu hình để lưu trữ trên một phân vùng riêng biệt để dễ dàng quản lý và sao lưu dữ liệu của người dùng.

# ***Thư mục nhị phân***
- Binary directories (thư mục nhị phân) trong Linux là nơi lưu trữ các tệp thực thi của hệ thống, bao gồm các lệnh, chương trình, tệp thư viện và các tệp nhị phân khác. Các thư mục nhị phân quan trọng nhất trong hệ thống Linux bao gồm:

`/bin`: Thư mục chứa các tệp thực thi cơ bản cho hệ thống, chẳng hạn như lệnh ls, cp, mv và rm.

`/sbin`: Thư mục chứa các tệp thực thi hệ thống quan trọng, được sử dụng để quản lý hệ thống, chẳng hạn như lệnh shutdown, ifconfig và iptables.

`/usr/bin`: Thư mục chứa các tệp thực thi cho các ứng dụng và chương trình không phải là cơ bản của hệ thống, chẳng hạn như lệnh grep, awk và sed.

`/usr/sbin`: Thư mục chứa các tệp thực thi hệ thống mở rộng, được sử dụng để quản lý hệ thống như lệnh useradd và networkd.

`/usr/local/bin`: Thư mục chứa các tệp thực thi được cài đặt bởi người dùng hoặc các gói cài đặt phụ trợ, chẳng hạn như lệnh git và pip.

`/usr/local/sbin`: Thư mục chứa các tệp thực thi hệ thống mở rộng được cài đặt bởi người dùng hoặc các gói cài đặt phụ trợ.

Các thư mục nhị phân được thêm vào biến PATH của hệ thống, cho phép các tệp thực thi được sử dụng một cách dễ dàng từ bất kỳ vị trí nào trên hệ thống. Các tệp thực thi trong các thư mục nhị phân được thực thi bằng cách sử dụng tên của chúng trong các lệnh dòng lệnh.

Thư mục /bin chứa các tệp nhị phân có thể thực thi, các lệnh cần thiết được sử dụng trong chế độ người dùng đơn, và các lệnh cần thiết được yêu cầu bởi tất cả người dùng hệ thống, chẳng hạn như ps, ls, cp. Các lệnh không cần thiết cho hệ thống trong chế độ người dùng đơn được đặt trong thư mục /usr/bin, trong khi thư mục /sbin được sử dụng cho các tệp nhị phân cần thiết liên quan đến quản trị hệ thống, chẳng hạn như ifconfig và shutdown. Cũng có một thư mục /usr/sbin cho các chương trình quản trị hệ thống ít quan trọng hơn. Tất cả các thư mục nhị phân đều nằm trong phân vùng gốc. Đôi khi /usr là một hệ thống tệp riêng biệt mà có thể không khả dụng trong chế độ người dùng đơn. Điều này là lý do tại sao các lệnh cần thiết đã được tách ra khỏi các lệnh không cần thiết. Tuy nhiên, trong một số hệ thống Linux hiện đại nhất, sự phân biệt này được coi là lỗi thời, và /usr/bin và /bin được liên kết với nhau cũng như /usr/sbin và /sbin.

# ***Thư mục thiết bị***
Thư mục /dev (device directory) trong Linux là nơi lưu trữ các tệp đại diện cho các thiết bị phần cứng của hệ thống. Trong hầu hết các trường hợp, các tệp trong /dev là các tệp đặc biệt được sử dụng để truy cập vào các thiết bị phần cứng.

Các thiết bị được đại diện bởi các tệp trong /dev có thể bao gồm ổ đĩa cứng, ổ đĩa CD/DVD, các thiết bị USB, các thiết bị âm thanh, các thiết bị mạng, các thiết bị nối tiếp và nhiều thiết bị khác.

Một số tệp thường gặp trong /dev bao gồm:

`/dev/sda`: Đại diện cho ổ đĩa cứng đầu tiên trong hệ thống.
`/dev/tty`: Đại diện cho thiết bị nối tiếp (serial) trên hệ thống.
`/dev/null`: Tệp này không phải là một thiết bị vật lý, nhưng được sử dụng để ghi thông tin đến nơi không bao giờ đọc được. Thông thường, tệp này được sử dụng để xóa dữ liệu một cách an toàn.
Các tệp trong /dev có thể được sử dụng để truy cập vào các thiết bị phần cứng bằng các lệnh dòng lệnh hoặc bởi các ứng dụng. Ví dụ, để xem nội dung của một ổ đĩa USB được gắn kết với /dev/sdb, bạn có thể sử dụng lệnh "sudo cat /dev/sdb".

Trong hệ thống Linux, các tệp trong /dev không thực sự lưu trữ dữ liệu về thiết bị phần cứng mà chỉ đại diện cho chúng. Các tệp này được tạo tự động khi hệ thống khởi động, và các tệp này sẽ thay đổi khi các thiết bị phần cứng được thêm hoặc loại bỏ khỏi hệ thống.
sudo cat /dev/sdb
# ***Thư mục biến***
Trong Linux, "variable directory" là một thuật ngữ dùng để chỉ một số thư mục chứa các tệp tin và thư mục có liên quan đến hệ thống. Các biến môi trường của hệ thống cũng được lưu trữ trong các thư mục này.

Các thư mục thường được coi là phần của variable directory là:
Thư mục /var chứa các tệp tin dự kiến sẽ thay đổi về kích thước và nội dung khi hệ thống đang chạy (var đứng cho biến) chẳng hạn như các mục trong các thư mục sau:
- `/var/log`: Chứa các tệp tin log của hệ thống và các ứng dụng. Các tệp tin này được sử dụng để theo dõi các sự kiện trên hệ thống.

- `/var/cache`: Chứa các tệp tin cache của ứng dụng, các gói cài đặt và các tệp tin khác liên quan đến bộ nhớ đệm của hệ thống.

- `/var/lib`: Chứa các tệp tin liên quan đến dữ liệu của ứng dụng, chẳng hạn như cơ sở dữ liệu và tệp tin cấu hình.

- `/var/run`: Chứa các tệp tin đang chạy của hệ thống và các ứng dụng. Các tệp tin này thường bị xóa khi hệ thống khởi động lại.

- `/var/spool`: Chứa các tệp tin liên quan đến bảng điều khiển đang chờ in hoặc gửi thư.

Thư mục /var có thể được đặt trong một phân vùng riêng để có thể điều chỉnh sự tăng trưởng của các tệp tin và kích thước tệp tin không ảnh hưởng nghiêm trọng đến hệ thống.
Các biến môi trường của hệ thống được lưu trữ trong các thư mục này, chẳng hạn như biến PATH (để chỉ định các đường dẫn mà hệ thống sẽ tìm kiếm các tệp lệnh) và biến LD_LIBRARY_PATH (để chỉ định các thư viện được sử dụng bởi các chương trình đang chạy).

Tổng quan, variable directory là những thư mục quan trọng trong Linux để lưu trữ các tệp tin, dữ liệu và biến môi trường của hệ thống và các ứng dụng.

# ***Thư mục cấu hình hệ thống***
Trong Linux, "system configuration directory" là một thuật ngữ dùng để chỉ các thư mục chứa các tệp tin cấu hình của hệ thống. Các tệp tin này thường được sử dụng để cấu hình các thiết lập của hệ thống và các ứng dụng.

Các thư mục thường được coi là phần của system configuration directory là:

- `/etc`: Là thư mục chứa các tệp tin cấu hình hệ thống và các ứng dụng. Các tệp tin trong thư mục này có thể được chỉnh sửa bởi quản trị viên hệ thống để tùy chỉnh hệ thống và các ứng dụng theo nhu cầu cụ thể.

- `/usr/share`: Là thư mục chứa các tệp tin chia sẻ của hệ thống. Các tệp tin này bao gồm các tài nguyên chia sẻ như icon, hình ảnh, âm thanh và các tệp tin cấu hình.

- `/usr/local/etc`: Là thư mục chứa các tệp tin cấu hình cho các ứng dụng cài đặt từ mã nguồn mở.

- `/opt`: Là thư mục chứa các ứng dụng và các tệp tin cấu hình liên quan đến các ứng dụng đó.

Các tệp tin cấu hình trong các thư mục này được sử dụng để cấu hình hệ thống, các ứng dụng, môi trường và các thiết lập khác của hệ thống. Ví dụ, các tệp tin cấu hình trong thư mục /etc được sử dụng để cấu hình các máy chủ, tường lửa, mạng, bảo mật và các thiết lập khác của hệ thống.

Tổng quan, system configuration directory là những thư mục quan trọng trong Linux để lưu trữ các tệp tin cấu hình của hệ thống và các ứng dụng, giúp quản trị viên hệ thống tùy chỉnh các thiết lập của hệ thống và các ứng dụng một cách dễ dàng.
# ***Thư mục khởi động***
Trong Linux, "boot directory" là một thư mục quan trọng được sử dụng để lưu trữ các tệp tin liên quan đến quá trình khởi động hệ thống. Thư mục này thường nằm trong phân vùng hệ thống.

Các tệp tin thường được lưu trữ trong thư mục boot là:

- `/boot/vmlinuz`: Đây là tệp tin nhân Linux, được sử dụng để khởi động hệ thống. Tệp tin này được tạo ra từ mã nguồn của nhân Linux và chứa mã máy thực thi.

- `/boot/initrd.img`: Đây là tệp tin hệ thống tệp hạt nhân gốc, được sử dụng để khởi động hệ thống và tải các module hạt nhân cần thiết.

- `/boot/grub/`: Đây là thư mục chứa các tệp tin cấu hình cho trình khởi động GRUB, được sử dụng để chọn hệ điều hành mà bạn muốn khởi động khi nhiều hệ điều hành được cài đặt trên cùng một máy tính.

- `/boot/System.ma`p: Đây là tệp tin bản đồ hệ thống, chứa một bản đồ địa chỉ của các hàm hạt nhân.

- `/boot/config`: Đây là tệp tin cấu hình của nhân Linux, chứa các thiết lập cơ bản cho nhân Linux được cài đặt.

Các tệp tin trong thư mục boot đóng vai trò quan trọng trong quá trình khởi động hệ thống. Khi hệ thống được khởi động, BIOS sẽ đọc tệp tin nhân Linux từ thư mục boot và bắt đầu quá trình khởi động hệ thống.

Tổng quan, boot directory là một thư mục quan trọng trong Linux để lưu trữ các tệp tin liên quan đến quá trình khởi động hệ thống. Các tệp tin trong thư mục boot giúp hệ thống được khởi động một cách thành công và ổn định.