# File path traversal, validation of file extension with null byte bypass

### Yêu cầu: Truy cập vào file /etc/passwd

### Hướng làm: 

Truy cập vào 1 file ảnh bất kì (không truy cập vào bài post vì bài post không được lưu trên hệ thống file server)

![image](https://user-images.githubusercontent.com/72268643/157159123-a3136fb2-7ce0-424d-98db-7960868a2980.png)

Khi sử dụng `../../../etc/passwd` ta không truy cập được vào vì có thể param yêu cầu file cuối cùng phải kết thúc bằng đuôi file `.jpg`.

Để bypass ta có thể dùng nullbyte `%00` trước `đuôi file`

`../../../etc/passwd%00.jpg`

![image](https://user-images.githubusercontent.com/72268643/157159533-957e4c95-d781-44bd-a067-026acf99e06c.png)

Hoàn thành lab
