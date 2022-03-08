# File path traversal, simple case

### Yêu cầu: truy cập vào file /etc/passwd

### Hướng làm: 

Trước tiên, ta sẽ phải truy cập vào 1 ảnh bất kì trên trang web (không truy cập vào bài post vì bài post không được lưu trực tiếp trên hệ thống file bên server)

![image](https://user-images.githubusercontent.com/72268643/157151490-c90b9f8d-58f3-4ba1-ae73-b338bb1f5233.png)

Ta có được đường dẫn tới ảnh `32.jpg`. Thay đổi file ảnh đó với `../../../etc/passwd` để truy cập tới địa chỉ cần đến và hoàn thành lab.
