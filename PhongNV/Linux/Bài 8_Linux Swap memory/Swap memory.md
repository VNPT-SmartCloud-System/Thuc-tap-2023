# ***Linux Swap memory***
Swap memory trong Linux là một phần của không gian đĩa được sử dụng để lưu trữ dữ liệu từ bộ nhớ RAM khi bộ nhớ đó đã được sử dụng hết. Khi bộ nhớ RAM không đủ để đáp ứng yêu cầu của các tiến trình đang chạy, kernel sẽ di chuyển các phần của bộ nhớ RAM đó vào Swap space. Swap space có thể là một phân vùng trên đĩa hoặc một tập tin trên hệ thống tệp.

Trong Linux, bạn có thể kiểm tra tình trạng swap space bằng lệnh `swapon -s`. Lệnh này sẽ liệt kê tất cả các swap file hoặc swap partition đang được sử dụng trên hệ thống của bạn.
![imag](./Img/9.png)
Bạn có thể tạo một swap partition mới bằng cách sử dụng các công cụ quản lý phân vùng như `fdisk, cfdisk, hoặc parted`. Sau khi tạo một swap partition mới, bạn cần định dạng nó với lệnh `mkswap` và kích hoạt swap partition mới với lệnh `swapon`.

Bạn cũng có thể tạo một tập tin swap bằng cách sử dụng lệnh `fallocate` hoặc `dd` để tạo một tập tin với kích thước cần thiết và sau đó định dạng tập tin đó với lệnh mkswap. Bạn cũng có thể kích hoạt tập tin swap mới với lệnh swapon.

Ngoài ra, bạn có thể tùy chỉnh cấu hình swap space bằng cách chỉnh sửa tập tin /etc/fstab. Trong tập tin này, bạn có thể định nghĩa các swap partition hoặc tập tin swap được sử dụng trên hệ thống của bạn, cũng như định cấu hình các thông số khác như ưu tiên và kích thước swap space.

1. Liệt kê tất cả các swap partition và swap file đang được sử dụng trên hệ thống của bạn:
`swapon -s`
2. Tạo một swap partition mới:
Sử dụng lệnh `fdisk` để tạo một partition mới:
`sudo fdisk /dev/sdb`
Chọn `n` để tạo một partition mới và làm theo các hướng dẫn để thiết lập kích thước và vị trí partition.

Chọn `t` để thiết lập loại partition là Linux swap.

Lưu lại các thay đổi với lệnh `w`.

Định dạng partition mới bằng lệnh `mkswap`:
`sudo mkswap /dev/sdb1`
Kích hoạt partition swap mới bằng lệnh swapon:`sudo swapon /dev/sdb1`
- Tạo một tập tin swap mới 
`sudo fallocate -l 2G /swapfile`
- Định dạng tập tin swap mới
`sudo mkswap /swapfile`
- Kích hoạt tập tin swap mới 
`sudo swapon /swapfile`

# ***Swap dimensioning***
Swap dimensioning là quá trình tạo và quản lý vùng swap trong hệ thống Linux. Vùng swap là một phần của đĩa cứng được sử dụng để lưu trữ dữ liệu khi hệ thống gặp phải tình huống không đủ bộ nhớ RAM để thực hiện các tác vụ.

, 
- Kiểm tra xem hệ thống đã có vùng swap hay chưa
`swapon -s`
- /etc/fstab: Cấu hình để hệ thống tự động mount vùng swap khi khởi động lại.
- /etc/sysctl.conf: Cấu hình để tăng kích thước vùng swap hoặc điều chỉnh thời gian hoạt động của swap.
- /proc/sys/vm/swappiness: Cấu hình để điều chỉnh cách hệ thống sử dụng vùng swap.
Tổng quan về swap dimensioning trên Linux như trên đây, tuy nhiên để cấu hình vùng swap một cách phù hợp cho hệ thống của bạn, bạn cần hiểu rõ các yêu cầu và tài nguyên của hệ thống để tối ưu hóa việc sử dụng vùng swap.
## ***bảng Swap***
Bảng Swap dimensioning trong Linux giúp ta xác định kích thước của vùng swap cần thiết cho hệ thống. Thông thường, kích thước vùng swap được tính toán dựa trên tổng số bộ nhớ RAM của hệ thống và các yếu tố khác như tải công việc và loại tác vụ được thực hiện trên hệ thống.

Dưới đây là một bảng Swap dimensioning được đề xuất cho các hệ thống Linux:

![imag](./Img/5.png)
Lưu ý rằng, bảng Swap dimensioning trên chỉ là một đề xuất và kích thước vùng swap cần thiết có thể khác nhau tùy thuộc vào yêu cầu cụ thể của hệ thống. Nếu bạn không sử dụng tính năng hibernation trên hệ thống của mình, bạn có thể cân nhắc giảm kích thước vùng swap. Ngược lại, nếu bạn thường xuyên sử dụng tính năng hibernation, bạn cần tăng kích thước vùng swap để đảm bảo có đủ không gian lưu trữ dữ liệu khi hệ thống vào chế độ hibernation.
# ***Add a swap area as a file***
Swap area là một phần của ổ cứng được sử dụng để lưu trữ các trang bộ nhớ tạm thời khi bộ nhớ RAM của hệ thống đã đầy. Trong Linux, bạn có thể tạo swap area bằng cách sử dụng một phân vùng hoặc một tệp swap. Trong trường hợp bạn không muốn tạo một phân vùng mới để sử dụng làm swap area, bạn có thể tạo một tệp swap để sử dụng thay thế. Bên dưới là hướng dẫn tạo tệp swap trong Linux:

Lưu ý rằng kích thước của tệp swap sẽ ảnh hưởng đến hiệu suất của hệ thống. Kích thước của tệp swap phải đủ lớn để đảm bảo rằng hệ thống có đủ không gian để lưu trữ các trang bộ nhớ tạm thời khi bộ nhớ RAM đã đầy. Tuy nhiên, quá nhiều tệp swap cũng có thể gây ra hiệu ứng phụ do quá trình swap in và swap out.
## ***Bộ nhớ tạm thời là gì***
Bộ nhớ tạm thời (hay còn gọi là bộ nhớ ảo hoặc swap) là một phần của bộ nhớ trong máy tính được sử dụng để lưu trữ dữ liệu tạm thời khi bộ nhớ chính (RAM) đã đầy hoặc không đủ để đáp ứng nhu cầu của các chương trình.

Khi bộ nhớ RAM đã đầy, hệ điều hành sẽ chuyển dữ liệu từ RAM vào bộ nhớ tạm thời để tạo thêm không gian cho các ứng dụng khác. Các trang bộ nhớ này sẽ được lưu trữ trên ổ cứng và được quản lý bởi hệ điều hành, sử dụng các thuật toán để quản lý việc chuyển đổi dữ liệu giữa bộ nhớ RAM và bộ nhớ tạm thời.

Tuy nhiên, việc sử dụng bộ nhớ tạm thời sẽ làm giảm hiệu suất của hệ thống, vì các trang bộ nhớ được chuyển đổi giữa RAM và bộ nhớ tạm thời sẽ tốn thời gian và tốn tài nguyên của ổ cứng. Do đó, nếu có thể, nên sử dụng đủ RAM để tránh sử dụng bộ nhớ tạm thời quá nhiều và giảm hiệu suất của hệ thống.