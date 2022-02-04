# YÊU CẦU: Tận dụng hàm thư viện JQuery để gọi hàm alert()

# Nguyên nhân:

Hàm `attr()` thay đổi các thuộc tính DOM và thẻ `href` sau khi submit feedback. Từ đó ta có thể tận dụng để thực thi các hàm.

# Hướng làm: 

Ta thấy ở chỗ `submit feedback` có nút `back`. Ta sẽ phải khai thác sao cho khi ấn nút `back` đó sẽ gọi hàm `alert()`

Để ý thấy biến `returnPath` sẽ trả về trang mà chúng ta muốn sau khi ấn nút `back`. 

![image](https://user-images.githubusercontent.com/72268643/152509039-d60d844e-a7b4-47c1-b89c-55560f8a2d69.png)

Thay vì để giá trị `/post`, ta thay thế bằng 1 chuỗi bất kì như `/abcd` rồi `Inspect` trang web đó. Kết quả là `abcd` được truyền và thẻ `href` và thực thi ở đó

![image](https://user-images.githubusercontent.com/72268643/152510550-09c04f2e-30d6-4b72-8580-d63a3e9ce79c.png)

Vậy chúng ta sẽ thay thế `/post` bằng `javascript:alert(document.cookie)` để thực thi hàm js đó và hoàn thành lab

![image](https://user-images.githubusercontent.com/72268643/152510849-14926cc1-b976-42bb-b79c-0d3085f82b52.png)
