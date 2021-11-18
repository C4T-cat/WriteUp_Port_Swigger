# Lab 2: Finding a column containing text

## Yêu cầu: Tìm trường dữ liệu có chứa thông tin yêu cầu

![image](https://user-images.githubusercontent.com/72268643/142391391-010f39de-977d-4a9b-9a63-e64f18286721.png)

## Bước làm: 

Đầu tiên xác định số trường dữ liệu tồn tại trong trang web như bài [Lab 1]() ta xác định được 3 trường dữ liệu

![image](https://user-images.githubusercontent.com/72268643/142391285-8017fcb9-607c-44f2-b9d5-590ab1325206.png)

Sau đó xác định xem cột nào có dữ liệu là **5HQ9ju** bằng cách thử: 

**'UNION select '5HQ9ju',NULL,NULL--** hoặc **'UNION select NULL,'5HQ9ju',NULL--** hoặc **'UNION select NULL,NULL,'5HQ9ju'--**

Ta có được thông báo hoàn thành lab với dữ liệu ở cột thứ 2 => DONE

![image](https://user-images.githubusercontent.com/72268643/142392570-48ee4a9f-e6fc-411b-92ba-dcdde64513a8.png)
