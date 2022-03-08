# File path traversal, traversal sequences stripped non-recursively

### Yêu cầu: truy cập vào file /etc/passwd

### Hướng làm: 

Trước tiên, ta sẽ phải truy cập vào 1 ảnh bất kì trên trang web (không truy cập vào bài post vì bài post không được lưu trực tiếp trên hệ thống file bên server).

![image](https://user-images.githubusercontent.com/72268643/157152487-5c314a2f-a7f0-4a03-a9cc-fa76a37afb76.png)

Ta có được đường dẫn tới ảnh `38.jpg`. Do ở đây trang web đã sử dụng các hàm để lọc các kí tự truyền vào như `../` và `..\`. 

Tuy nhiên do hàm lọc này duyệt các kí tự như 1 vòng for đơn nên với trường hợp `....//` hoặc `...\./` thì trang web sẽ chỉ loại bỏ các kí tự ở giữa và sau khi duyệt xong ta sẽ được `../` hợp lệ

Vậy ta truyền vào `....//....//....//etc/passwd` để hoàn thành lab.

![image](https://user-images.githubusercontent.com/72268643/157154787-4ba93920-c1c4-47ff-8550-e1fc48a9b539.png)
