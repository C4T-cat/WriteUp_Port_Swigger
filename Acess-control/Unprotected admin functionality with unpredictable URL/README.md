# YÊU CẦU: Truy cập vào trang quản lý của admin và xóa người dùng `carlos`

# NGUYÊN NHÂN: Tuy đã bảo mật được các trang cũng như là các file nhạy cảm nhưng lại để lộ các đoạn code trong URL người dùng có liên quan đến trang quản lý

# WRITEUP: 

Đầu tiên, ta mở source code thì thấy có một đoạn code JS như sau:

![image](https://user-images.githubusercontent.com/72268643/150748310-f50a349a-613a-4a1a-9835-83e59da15dfb.png)

chúng ta thấy URL được set thêm với giá trị `/admin-3xcb9h` để cho người dùng bình thường không đoán được.

Thử truy cập vào trang đó, ta có được quyền xóa tài khoản của admin. Sau đó xóa tài khoản và hoàn thành lab.

![image](https://user-images.githubusercontent.com/72268643/150748371-e028bee4-f639-4d1d-a4c6-b2a5d63be1a5.png)
