# YÊU CẦU: Gọi hàm `alert()`

# HƯỚNG LÀM: 

Bài này chúng ta sẽ vẫn dụng hàm `innerHTML` truyển kết quả tìm kiếm và qua đó để thực hiện XSS

![image](https://user-images.githubusercontent.com/72268643/151292288-6e034c8c-500f-412a-af52-a20a73ec5b41.png)

Đoạn này ta có thể sử dụng cái hàm như img, svg (không hiểu sao trong phần lý thuyết họ lại bảo không dùng được), iframe để thực hiện lệnh XSS

![image](https://user-images.githubusercontent.com/72268643/151292588-4af376c3-dda8-4947-a2ce-5631d78a4e47.png)

`<svg onload=alert(1)>` => Hoàn thành lab
