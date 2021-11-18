# Lab 4: Retrieving multiple values in a single column

## Yêu cầu: 

Lấy tài khoản của *administrator* để đăng nhập

## Writeup: 

Đầu tiên xác định số trường dữ liệu với **'UNION SELECT .... FROM users--** , ta có được là 2 

![image](https://user-images.githubusercontent.com/72268643/142468653-a6b5ef39-df06-41e2-bef7-b6f9f405ef71.png)

Tiếp đến xét xem cột nào có chứa dữ liệu ở cột 1 hoặc cột 2, t có kết quả dữ liệu ở cột 2

![image](https://user-images.githubusercontent.com/72268643/142469011-618f519f-f377-44f6-82bc-0d8a7802327e.png)

Vậy để lấy dữ liệu, t phải gộp dữ liệu **username** và **password** vào cột 2 với **'UNION SELECT NULL,username || '~' || password FROM users--**

![image](https://user-images.githubusercontent.com/72268643/142469938-a7a281f6-2c99-4a41-ad5d-75d510e70136.png)

Ta có password của *administrator* để đăng nhập => ***DONE***
