# Yêu cầu: Gọi hàm print() bằng XSS

Đầu tiên, chúng ta sẽ thử với tag cơ bản là `<button onclick="window.print()">Print this page</button>`

![image](https://user-images.githubusercontent.com/72268643/150565584-bda29dcc-a7eb-4035-9421-f6d790f00e25.png)

Như đề bài có nói, WAF đã chặn hầu hết các tag, vậy chúng ta cần phải tìm xem tag nào ko bị chặn. 

Để làm được thì Brute Force tất cả các tag đã được liệt kê trong [XSS Cheat Sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet#waf-bypass-global-objects)

![image](https://user-images.githubusercontent.com/72268643/150566110-4884b486-7244-420b-9b56-46ce431ad510.png)

Sau đó paste ra Notepad rồi lưu, tiếp đến sử dụng Burp Suit để thực hiện Brute và tìm cho đến khi không thấy cụm từ `Tag is not allowed` (tức là tag đó không bị báo lỗi)

![image](https://user-images.githubusercontent.com/72268643/150574072-028ba39d-d83a-43f0-8c2e-de2ffb32d365.png)

Vậy là thẻ `body` không bị chặn. Tiếp đến chúng ta sẽ là tương tự với các event để tìm event ko bị chặn
  
![image](https://user-images.githubusercontent.com/72268643/150578589-4e4d45bd-7902-4333-b489-375863cc5f17.png)
  
![image](https://user-images.githubusercontent.com/72268643/150577096-c81374b0-a554-4656-9bc8-885a9be03b8b.png)

Vậy thẻ `body` và event `onresize` không bị chặn.  

Chúng ta sẽ thử câu lệnh `<body onresize=alert(1)>` để xem việc XSS có thành công không

![image](https://user-images.githubusercontent.com/72268643/150580289-dd03906c-7aac-41e7-b0bb-4611a2491df6.png)

Kết quả: event `onresize` chỉ xảy ra khi thay đổi kích thước trình duyệt -> thành công

![image](https://user-images.githubusercontent.com/72268643/150580397-7ad37ab8-d313-47f4-a9e5-bf1ee55d9ba3.png)

Bước cuối cùng, chúng ta sẽ exploit server để hiển thị câu lệnh tấn công XSS với thẻ `iframe` cùng với nội dung `"><body onresize=print()>` đã được **encode URL** 
(Đoạn thêm vào `onload` mình cũng chưa thực sự hiểu lắm nên có đi lướt comment và tìm được [1 vid giải thích ở phút thứ 16](https://www.youtube.com/watch?v=YN1SCj6_cU0))

![image](https://user-images.githubusercontent.com/72268643/150583237-52074334-db86-48fb-b8e5-14d6924c7e6e.png)

Sau đó Store và Deliver exploit to victim -> Hoàn thành lab
