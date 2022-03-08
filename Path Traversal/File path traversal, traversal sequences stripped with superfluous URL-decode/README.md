# File path traversal, traversal sequences stripped with superfluous URL-decode

### Yêu cầu: truy cập vào file /etc/passwd

### Hướng làm: 

Trước tiên, ta sẽ phải truy cập vào 1 ảnh bất kì trên trang web (không truy cập vào bài post vì bài post không được lưu trực tiếp trên hệ thống file bên server)

![image](https://user-images.githubusercontent.com/72268643/157152487-5c314a2f-a7f0-4a03-a9cc-fa76a37afb76.png)

Ta có được đường dẫn tới ảnh `38.jpg`. ta không thể truy cập vào `/etc/passwd` bằng `../` được vì param `filename` là dạng `multipart/form-data` nên nó sẽ loại bỏ các kí tự đó

Ta có thế bypass bằng cách sử dụng URL encode hoặc URL encode kép (thay vì truyền vào `../` thì ta truyền vào `..%2F` hoặc `..%252F`)

Qua đó, ta sẽ sử dụng `..%2F..%2F..%2Fetc%2Fpasswd` hoặc `..%252F..%252F..%252Fetc%252Fpasswd` để truyền vào.

![image](https://user-images.githubusercontent.com/72268643/157156724-23911e36-9663-494d-b7af-ba904f1b8bda.png)
 
Hoàn thành lab.
