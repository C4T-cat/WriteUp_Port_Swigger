# File path traversal, traversal sequences blocked with absolute path bypass

### Yêu cầu: truy cập vào file /etc/passwd

### Hướng làm: 

Trước tiên, ta sẽ phải truy cập vào 1 ảnh bất kì trên trang web (không truy cập vào bài post vì bài post không được lưu trực tiếp trên hệ thống file bên server)

![image](https://user-images.githubusercontent.com/72268643/157152810-c0c3d444-35b1-4909-8c71-c509e520246c.png)

Ta có được đường dẫn tới ảnh `38.jpg`. Nếu thay đổi file ảnh đó với `../../../etc/passwd` để truy cập thì ta sẽ được kết quả sau:

![image](https://user-images.githubusercontent.com/72268643/157153020-d628c0f8-030b-44fb-b55c-2ed02eeb0889.png)

Ta không truyền vào được vì ở đây trang web yêu cầu ta truyền vào 1 file tuyệt đối (đường dẫn tới file đó) nên chắc chắc các kí tự `../` sẽ không có nghĩa.

Do đó, ta chỉ cần truyền vào param là `/etc/passwd` để hoàn thành lab :)
