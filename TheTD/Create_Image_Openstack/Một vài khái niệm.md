#  Khái niệm

- Đóng image là gì ?

Quá trình đóng image (image building) là quá trình tạo ra một file image có thể sử dụng được để triển khai máy ảo (virtual machine) hoặc container. Quá trình này bao gồm việc tạo một máy ảo hoặc container cơ bản, cài đặt các gói phần mềm, cấu hình hệ thống, cài đặt các ứng dụng và tinh chỉnh hệ thống để đáp ứng nhu cầu cụ thể.

Quá trình đóng image thường được thực hiện để tạo ra các image chuẩn hoặc image tùy chỉnh để sử dụng cho triển khai máy ảo hoặc container nhanh chóng và đáng tin cậy hơn. Quá trình này cũng có thể giúp tối ưu hóa kích thước của image và đảm bảo tính bảo mật của image được triển khai

- Các bước thực hiện đóng image

1. Tạo một máy ảo mới từ file ISO của hệ điều hành cần cài đặt.
2. Cài đặt các gói phần mềm cần thiết cho hệ điều hành trên máy ảo.
3. Xóa toàn bộ thông tin nhận dạng và cấu hình mạng của máy ảo bằng lệnh virt-sysprep.
4. Tạo snapshot cho máy ảo để lưu lại trạng thái hiện tại.
5. Xóa các file log và các gói cài đặt không cần thiết.
6. Thực hiện tối ưu kích thước ổ đĩa của máy ảo bằng lệnh virt-sparsify.
7. Tạo file image từ ổ đĩa của máy ảo bằng lệnh qemu-img.
8. Upload file image lên OpenStack Glance bằng lệnh glance image-create.

Sau khi hoàn thành các bước trên, ta sẽ có một image hoàn chỉnh và tối ưu để sử dụng trên nền tảng OpenStack.

- Một số khái niệm:
1. Sysprep: Sysprep là một công cụ của Microsoft Windows, cho phép bạn loại bỏ các thông tin máy tính đặc trưng như tên máy tính, địa chỉ IP, thông tin người dùng và các giá trị khác. Việc thực hiện Sysprep giúp cho image có thể tái sử dụng được cho nhiều máy tính khác nhau mà không cần phải cấu hình lại.

2. Cloud-init: Cloud-init là một công cụ được sử dụng để cấu hình các máy ảo trên các hệ thống điện toán đám mây. Nó cung cấp các thông tin cấu hình và script để tự động hóa quá trình cấu hình máy ảo, bao gồm cả việc đặt mật khẩu, thiết lập mạng, cài đặt phần mềm và các tùy chỉnh khác.

3. Virt-sysprep: Virt-sysprep là một công cụ dòng lệnh được sử dụng để chuẩn bị máy ảo cho việc sao chép hoặc phân phối. Nó giúp loại bỏ thông tin đặc trưng của máy tính, tạo ra một bản sao không chứa thông tin cụ thể và làm cho máy ảo trở thành một bản sao chính xác của hệ thống gốc.

4. Glance: Glance là một dịch vụ trên OpenStack, được sử dụng để quản lý các image máy ảo. Glance cho phép người dùng tạo, tải lên và chia sẻ các image máy ảo với các người dùng khác trên hệ thống OpenStack.

- Một số lưu ý

1. Chọn đúng hệ điều hành và phiên bản: Kiểm tra và chọn phiên bản hệ điều hành phù hợp để đóng image, đảm bảo rằng phiên bản này có hỗ trợ cho việc chạy trên cloud và các môi trường ảo hóa khác.

2. Làm sạch các thông tin nhạy cảm: Trước khi đóng image, cần đảm bảo rằng các thông tin nhạy cảm như tài khoản, mật khẩu, khóa SSH, dữ liệu người dùng, v.v. đã được xóa sạch. Nếu không làm sạch các thông tin này, thông tin nhạy cảm có thể bị lộ ra ngoài và gây ra rủi ro bảo mật.

3. Cập nhật các gói phần mềm và bảo mật: Trước khi đóng image, nên cập nhật các gói phần mềm và bảo mật lên phiên bản mới nhất để đảm bảo rằng image có thể chạy được trên các môi trường ảo hóa mới nhất và giảm thiểu các rủi ro bảo mật.

4. Kiểm tra kích thước và dung lượng ổ đĩa: Đảm bảo rằng kích thước và dung lượng ổ đĩa của image là phù hợp với các yêu cầu của môi trường ảo hóa. Nếu dung lượng ổ đĩa quá lớn, nó có thể làm chậm quá trình triển khai.

5. Thực hiện kiểm tra và xóa các file log: Các file log có thể chứa thông tin nhạy cảm hoặc dữ liệu cá nhân. Vì vậy, trước khi đóng image, cần kiểm tra và xóa các file log không cần thiết.

6. Sử dụng các công cụ và lệnh tối ưu hóa image: Sử dụng các công cụ và lệnh tối ưu hóa image để giảm kích thước của image và tăng tốc độ triển khai. Các công cụ và lệnh này có thể khác nhau tùy thuộc vào hệ điều hành và môi trường ảo hóa được sử dụng.

- Một số định dạng phổ biến:

1. RAW: định dạng này lưu trữ dữ liệu của image dưới dạng không nén và không được mã hóa. Đây là định dạng thông dụng nhất cho ảo hóa và có thể được sử dụng trên hầu hết các hypervisor.

2. Qcow2: định dạng này được sử dụng trong KVM và hỗ trợ tính năng như snapshot, nén, mã hóa và hiệu suất tốt hơn so với định dạng RAW. Tuy nhiên, độ tin cậy của Qcow2 không cao bằng RAW.

3. VMDK: định dạng này được sử dụng trong VMware và hỗ trợ tính năng như snapshot, mã hóa và các tính năng bảo mật khác.

4. VDI: định dạng này được sử dụng trong VirtualBox và hỗ trợ tính năng snapshot, mã hóa và hiệu suất tốt hơn so với định dạng RAW.

5. ISO: định dạng này được sử dụng để tạo các image bootable để cài đặt hệ điều hành hoặc phần mềm trên các máy ảo.

Các định dạng image khác cũng được sử dụng nhưng chúng thường ít phổ biến hơn và được sử dụng trong các trường hợp cụ thể. Các định dạng này bao gồm VHDX, QCOW, VHD, và nhiều hơn nữa.