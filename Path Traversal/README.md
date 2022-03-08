# Path Traversal

### 1) Path Traversal là gì ❓
Directory traversal, hay còn gọi là Path traversal, là một dạng tấn công cho phép hacker truy cập vào các thư mục và tập tin cấm trên máy chủ. Nếu như truy cập thành công thì hacker có thể xem được các file, thư mục cấm và thực thi các câu lệnh trên máy chủ. Nó dẫn đến việc bị lộ thông tin nhạy cảm của ứng dụng như thông tin đăng nhập , một số file hoặc thư mục của hệ điều hành. Trong một số trường hợp cũng có thể ghi vào các files trên server, cho phép kẻ tấn công có thể thay đổi dữ liệu hay thậm chí là chiếm quyền điều khiển server.

### 2) Phát hiện Path Traversal 🔎
Giả sử chúng ta có 1 trang web đang gửi truy vấn là: `http://wjbu.com/Loader?filename=123.png` tức là ta đang truy cập đến ảnh theo đường dẫn `var/www/images/123.png`

Với hướng đó, ta có thể sử dụng `../` để trở về thư mục gốc và truy cập sang các file khác như sau: `http://wjbu.com/Loader?filename=../../../etc/passwd`

Lúc đó Trang web sẽ hiểu `../` có nghĩa là trả về thư lục trước đó. Từ đó chúng ta trở về thư mục gốc rồi truy cập vào file `/etc/passwd`

**LƯU Ý:** Đối với hệ điều hành dựa trên Unix, file `/etc/passwd` là file chứa các thông tin về người dùng. Đối với hệ điều hành Windows thì ta có thể sử dụng `..\` để tương đương `../` và truy cập vào file `\windows\win.ini` để có được thông tin tương tự.

### 3) Khai thác Path Traversal ⚔
Lỗ hổng này khiến cho việc bảo mật các thông tin nhạy cảm của người dùng với các file của hệ thống. Hacker có thể xem các dữ liệu đó, thậm chí thay đổi các file quan trọng và có thể dẫn đến việc mất quyền kiểm soát hệ thống.

### 4) Ngăn chặn Path Traversal 🛡
Cách hiệu quả nhất để ngăn chặn các lỗ hổng directory traversal là **tránh chuyển hoàn toàn đầu vào do người dùng cung cấp tới API**. Nếu việc chuyển đầu vào do người dùng cung cấp tới hệ thống API được coi là không thể tránh khỏi, thì nên sử dụng hai lớp phòng thủ để ngăn chặn các cuộc tấn công:
  +) Nên validate input của người dùng trước khi xử lý nó.
  +) Sử dụng whitelist cho những giá trị được cho phép.
  +) Hoặc tên file là những kí tự số, chữ không nên chứa những ký tự đặc biệt.

### 5) Writeup các lab trên PortSwigger

| Tình trạng | Tên |
|:-:|-|
| ✔ | [File path traversal, simple case](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal%2C%20simple%20case) |
| ✔ | [File path traversal, traversal sequences blocked with absolute path bypass](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal%2C%20traversal%20sequences%20blocked%20with%20absolute%20path%20bypass) |
| ✔ | [File path traversal, traversal sequences stripped non-recursively](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal%2C%20traversal%20sequences%20stripped%20non-recursively) |
| ✔ | [File path traversal, traversal sequences stripped with superfluous URL-decode](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal%2C%20traversal%20sequences%20stripped%20with%20superfluous%20URL-decode) |
| ✔ | [File path traversal, validation of start of path](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal%2C%20validation%20of%20file%20extension%20with%20null%20byte%20bypass) |
| ✔ | [File path traversal, validation of file extension with null byte bypass](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Path%20Traversal/File%20path%20traversal,%20validation%20of%20file%20extension%20with%20null%20byte%20bypass) |

