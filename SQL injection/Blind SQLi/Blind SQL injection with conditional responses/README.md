**Yêu cầu: Truy vấn qua Cookies và đăng nhập vào bằng tài khoản của administrator

Đầu tiên chúng ta sẽ chặn truy vấn bằng Burp Suit sau đó gửi đến Repeater để xử lý các bước tiếp theo.

Sau khi có được truy vấn, chúng ta gửi câu truy vấn bằng cách sửa giá trị của Cookie `TrackingId` là `cookie_value' AND 1='1` 

![image](https://user-images.githubusercontent.com/72268643/150344488-92ced1db-0dc1-46cc-a3c0-5eb70b5551f4.png)

Sau khi gửi lại thì tìm thử cụm từ `Welcome back` thì thấy có xuất hiện chứng tỏ truy vấn đã thành công

Tiếp đến, vì đầu bài đã cho biết có 1 bảng `users` vs 2 trường là `username` và `password` nên ta sẽ thử truy vấn tới đó với câu lệnh 
`cookie_value' AND (SELECT 'a' FROM users WHERE username='administrator')='a`

![image](https://user-images.githubusercontent.com/72268643/150340684-8a64a975-a8f5-4dd5-84ac-e924f333377e.png)

Truy vấn thành công. Tiếp đến là công việc dò mật khẩu. Trước tiên cần phải biết độ dài của mật khẩu đó bằng cách truy vấn với 
`cookie_value' (SELECT 'a' FROM users WHERE (username='administrator' AND length(password)=psw_length)='a` (`psw_length` là tham số cần truyền vào)

Sau đó dùng Intruder để bruteforce tham số `psw_length` cho đến khi tìm thấy cụm từ `Welcome back`

![image](https://user-images.githubusercontent.com/72268643/150339590-0bdfbee6-e16f-471d-b378-260ad85bd5e4.png)

Vậy độ dài của password là 20 ký tự (dài thế @@)

Tiếp đến là bước dò mật khẩu. Với 20 kí tự thì cách dò từng từ bằng câu lệnh `cookie_value' AND SUBSTRING((SELECT password FROM users WHERE username = 'administrator'), 1, 1) = 'value` chúng ta sẽ sử dụng Burp Suit để Brute mật khẩu (cụ thể là brute từng kí tự thay vì brute cả mật khẩu (62^20 ký tự thì lâu quá)).

![image](https://user-images.githubusercontent.com/72268643/150338113-65165827-11c6-46ce-a6c7-f84944cbb1d3.png)

Vậy kí tự đầu tiên `6`. Ta sẽ làm tương tự cho đến kí tự thứ 20 thì được: **61jbw9rnfx6odplfem29**

Đăng nhập vào tài khoản của `administrator` với mật khẩu trên, ta sẽ hoàn thành được lab.
