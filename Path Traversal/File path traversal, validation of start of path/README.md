# File path traversal, validation of start of path

### Yêu cầu: truy cập vào file /etc/passwd

### Hướng làm: 

Trước tiên, ta sẽ phải truy cập vào 1 ảnh bất kì trên trang web (không truy cập vào bài post vì bài post không được lưu trực tiếp trên hệ thống file bên server)

![image](https://user-images.githubusercontent.com/72268643/157157915-9d923c54-55fe-4322-a73c-6fe529fb332e.png)

Ở đây param `filename` yêu cầu truyền vào 1 đường dẫn đúng như `/var/www/images/37.jpg` (tính từ file thư mục gốc)

Vậy nên để truy cập thư mục khác, ta sẽ bắt đầu bằng `/var/www/images` sau đó thêm 3 `../` để trả về thư mục gốc và truy cập vào `/etc/passwd`

`/var/www/images/../../../etc/passwd`

![image](https://user-images.githubusercontent.com/72268643/157158344-0198543a-6fc7-4b31-8fcc-e7e8be1dc428.png)

Hoàn thành lab.
