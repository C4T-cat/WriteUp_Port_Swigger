# Lab 6: SQL injection attack, querying the database type and version on Oracle

## Yêu cầu: 

Hiển thị thông tin phiên bản Oracle

## Writeup: 

Đầu tiên xác định số cột dữ liệu với **'UNION SELECT .... FROM users--** , ta có được là 2 

![image](https://user-images.githubusercontent.com/72268643/147381893-ac5f66df-a404-4e3c-aa75-a85bba17ca33.png)

Tiếp đến xét xem cột nào có chứa dữ liệu ở cột 1 hoặc cột 2, t có kết quả dữ liệu ở cả 2 cột

![image](https://user-images.githubusercontent.com/72268643/147382388-80303aa7-a443-44ac-9bc9-ddef4e7a9bb7.png)

![image](https://user-images.githubusercontent.com/72268643/147382390-3f8c8a24-493c-43fc-84e9-388ceb6277f0.png)

Do đây không sử dụng Oracle nên chúng ta sẽ thử tìm *version()* hoặc *@@version* để xác định phiên bản

![image](https://user-images.githubusercontent.com/72268643/147382428-284af8b6-56a1-47a7-8103-a2bab8c4d0d2.png)

![image](https://user-images.githubusercontent.com/72268643/147382454-cbf7be0d-2e05-444f-b495-14b2650876ca.png)

Chúng ta có được thông tin phiên bản **PostgreSQL**

-> **DONE**



