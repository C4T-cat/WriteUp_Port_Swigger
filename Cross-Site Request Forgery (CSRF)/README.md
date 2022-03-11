# Cross-Site Request Forgery CSRF

### 1) CSRF là gì ❓
CSRF (Cross Site Request Forgery) là kỹ thuật tấn công bằng cách **sử dụng quyền chứng thực của người dùng đối với một website.** CSRF là kỹ thuật tấn công vào người dùng, dựa vào đó hacker có thể thực thi những thao tác phải yêu cầu sự chứng thực. Hiểu một cách nôm na, đây là kỹ thuật tấn công dựa vào mượn quyền trái phép.

### 2) Phát hiện CSRF 🔎
Có thể sử dụng nhiều tài khoản ở các mức độ khác nhau để thực hiện việc thay đổi cookie/session giữa các tài khoản người dùng nhằm kiểm tra các lỗ hổng trong việc xác thực.
  
### 3) Khai thác CSRF ⚔
Để thực hiện tấn công này thì chúng ta cần phải có 3 điều kiện:
  - Nạn nhân phải thực hiện các hành động như sửa đổi thông tin hay sửa đổi đặc quyền cho chủ thể khác (đăng bài, thay đổi email, nâng quyền người dùng,...)
  - Để thực hiện được HTTP request phải dựa vào xử lý phiên trên cookies cùng với trang web đó phải không có xác thực người dùng.
  - Không có các thông số đoán trước không có cơ sở (chẳng hạn như thay đổi mật khẩu thì phải có mật khẩu hiện tại)

Khi đã có đủ điều kiện này, người dùng có thể chịu các mất mát sau: 
  +) Đánh cắp dữ liệu, tài sản quan trọng của nạn nhân.
  +) Thực hiện các hành động đặc quyền trên các tài khoản quan trọng bị CSRF.
  +) Gây ra các Worm trên các nền tảng MXH, dễ dàng mở rộng phạm vị với các file mã động được đính kèm.

### 4) Ngăn chặn CSRF 🛡
  a) Phía User
    - Không click vào các đường dẫn lạ.
    - Đăng xuất khỏi các tài khoản quan trọng mỗi khi dùng xong cũng như hạn chế việc lưu mật khẩu.
    - Khi thực hiện các thao tác quan trọng thì không nên vào các trang web khác.
    - Bảo vệ người thân xung quanh bằng việc tuyên truyền các điều trên
    
  b) Phía Client
    - Sử dụng GET và POST đúng cách. Dùng GET nếu thao tác là truy vấn dữ liệu (nên thường không dùng token để xác thực). Dùng POST nếu các thao tác tạo ra sự thay đổi hệ thống.
    - Thực hiện các bước xác thực người dùng khác như gửi capcha, thông báo xác nhận qua email, số điện thoại.
Sử dụng Token: 
    - Tạo ra một token tương ứng với mỗi form, token này sẽ là duy nhất đối với mỗi form và thường thì hàm tạo ra token này sẽ nhận đối số là "SESSION" hoặc được lưu thông tin trong SESSION. Khi nhận lệnh HTTP POST về, hệ thống sẽ thực hiện so khớp giá trị token này để quyết định có thực hiện hay không. Mặc định trong Rails, khi tạo ứng dụng mới:
      ```    
      class ApplicationController < ActionController::Base
        protect_from_forgery with: :exception
      end
      ```
    - Khi đó tất cả các form và Ajax request được tự động thêm security token generate bởi Rails. Nếu security token không khớp, exception sẽ được ném ra.
    - Sử dụng SameSite Cookie để kiểm tra người dùng:
      ```
        Set-Cookie: CookieName=CookieValue; SameSite=Lax;
      Set-Cookie: CookieName=CookieValue; SameSite=Strict;
      ```
    - Kiểm tra IP của tài khoản người dùng cùng với các request khác.

### 5) Writeup các lab trên PortSwigger

| Tình trạng | Tên |
|:-:|-|
| ✔ | [CSRF vulnerability with no defenses](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20vulnerability%20with%20no%20defenses) |
| ✔ | [CSRF where token validation depends on request method](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20token%20validation%20depends%20on%20request%20method) |
| ✔ | [CSRF where token validation depends on token being present](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20Referer%20validation%20depends%20on%20header%20being%20present) |
| ✔ | [CSRF where token is not tied to user session](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20token%20is%20not%20tied%20to%20user%20session) |
| ✔ | [CSRF where token is tied to non-session cookie](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20token%20is%20tied%20to%20non-session%20cookie) |
| ✔ | [CSRF where token is duplicated in cookie](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20token%20is%20duplicated%20in%20cookie) |
| ✔ | [CSRF where Referer validation depends on header being present](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20where%20token%20validation%20depends%20on%20token%20being%20present) |
| ✔ | [CSRF with broken Referer validation](https://github.com/C4T-cat/WriteUp_Port_Swigger/tree/main/Cross-Site%20Request%20Forgery%20(CSRF)/CSRF%20with%20broken%20Referer%20validation) |
