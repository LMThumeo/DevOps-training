# Process & Package

## I. Process

### 1. ps (process)

- **ps** Tiến trình (process) là các chương trình đang chạy trên máy. Chúng được quản lí bởi hạt nhân và mỗi tiến trình có một ID riêng (PID)

  ![ps](picture/ps.png)

- Các phần từ trái qua phải:

  - PID: ID quy trình

  - TTY: kiểm soát thiết bị đầu cuối liên quan đến quy trình

  - TIME: tổng thời gian sử dụng CPU

  - CMD: Tên của lệnh, lệnh thực thi

- Flag

  - **a** hiển thị tất cả các quá trình đang chạy , bao gồm cả những quá trình đang được chạy vởi những người dùng khác

  - **u** đưa ra chi tiết hơn về các tiến trình

  - **x** liệt kê tất cả các quy trình không có TTY liên kết với nó, các chương trình này sẽ thể hiện *?* ở trường TTY

  ![psaux](picture/psaux.png)

- Ngoài ra, lệnh **top** cung cấp thông tin thời gian thực về các tiến trình đang chạy trên hệ thống. Đây là công cụ hữu ích để xem những quy trình nào đang chiếm

  ![top](picture/top.png)

### 2. Process Details

- Kernel phụ trách các tiến trình, khi chúng ta chạy một chương trình, kernel sẽ tải mã của chương trình đó lên bộ nhớ, xác định và phân bổ tài nguyên, giữ các tab trên mỗi tiến trình. Nó biết:

  - Tình trạng của tiến trình

  - Các tài nguyên mà tiến trình nhận được và đang sử dụng

  - Chủ sở hữu của tiến trình

  - Xử lí tín hiệu

  - Mọi thứ cơ bản khác

- Khi một tiến trình kết thúc, tài nguyên nó sử dụng sẽ được giải phóng cho tiến trình khác.

- VD: Mở 3 terminal, ở 2 terminal, chạy lệnh ```cat``` nhưng ko có đối số. Ở cửa sổ còn lại, chạy lệnh ```ps aux | grep cat```. Bạn sẽ thấy 2 tiến trình cho lệnh **cat** mặc dù nó gọi tới cùng một chương trình.

  ![3terminal](picture/3terminal.png)

### 3. Process Creation

- Khi một tiến trình mới được tạo, một tiến trình hiện có sẽ tự sao chép bằng cách sử dụng fork system call. Fork system call sẽ tạo một tiến trình con gần như giống hệt và nó có mã tiến trình mới (PID). Tiến trình gốc sẽ trở thành "tiến trình cha" của nó và. Tiến trình con sẽ có mã tiến trình cha kí hiệu là PPID.

  ![ps-l](picture/ps-l.png)