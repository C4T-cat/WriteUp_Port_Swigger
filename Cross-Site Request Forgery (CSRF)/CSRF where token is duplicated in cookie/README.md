# CSRF where token is duplicated in cookie

### Yêu cầu: Tạo thẻ HTML để tấn công CSRF thay đổi email của tài khoản người dùng

### Hướng làm: 

Đầu tiên ta đăng nhập vào tài khoản `wiener:peter` rồi thay đổi mail bằng 1 mail bất kì và bắt request đó.

![image](https://user-images.githubusercontent.com/72268643/157429792-29964f06-99a8-41d6-b424-19255aed0982.png)

Để làm được bài này ta có thể vẫn sử dụng method POST và xóa đi param `csrf` đi và có thể gửi được request thành công.
