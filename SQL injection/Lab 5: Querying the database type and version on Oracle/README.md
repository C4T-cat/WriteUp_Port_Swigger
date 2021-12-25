# Lab 5: SQL injection attack, querying the database type and version on Oracle

## Yêu cầu: 

Hiển thị thông tin phiên bản Oracle

## Writeup: 

Đầu tiên xác định số cột dữ liệu với **'UNION SELECT .... FROM users--** , ta có được là 2 

![image](https://user-images.githubusercontent.com/72268643/147381893-ac5f66df-a404-4e3c-aa75-a85bba17ca33.png)


Tiếp đến xét xem cột nào có chứa dữ liệu ở cột 1 hoặc cột 2, t có kết quả dữ liệu ở cả 2 cột

![image](https://user-images.githubusercontent.com/72268643/147381913-b995faec-5796-4586-85fa-6d8d0adea409.png)

![image](https://user-images.githubusercontent.com/72268643/147381942-126aac6a-4b48-46a0-925a-bc572175a13d.png)

Vậy để lấy được thông tin phiên bản Oracle t sẽ thử truy vấn *banner* ở 1 trong 2 cột dữ liệu đó bằng câu lệnh 	**'UNION SELECT banner,NULL FROM v$version--**

![image](https://user-images.githubusercontent.com/72268643/147382014-ce175b32-b1ed-41b4-b510-4818d85681dd.png)

![image](https://user-images.githubusercontent.com/72268643/147382026-c13c5b51-05d6-48ec-9a09-21c15fb004ba.png)

-> **DONE**
