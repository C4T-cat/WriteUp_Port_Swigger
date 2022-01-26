# YÊU CẦU: Gọi hàm `alert()`

# HƯỚNG LÀM: 

Đầu tiên, do không có thanh search nên chúng ta sẽ thử vào 1 mặt hàng bất kì. Cũng không thấy có thanh truyền vào nhưng ta lại có trường chọn các giá trị

![image](https://user-images.githubusercontent.com/72268643/151229357-a6dca438-6645-4364-bda6-809f1b78b209.png)

Kết quả chúng ta chọn sẽ được truyền vào trong câu `document.write('<select name="storeId">');`

Vậy nên, về cơ bản lab này giống lab trước, nhưng lại không có thanh công cụ search để truyền vào mà phải truyền thông qua URL vào `storeId`.

Thêm 1 điều nữa, để đóng thẻ `<select>` thì chúng ta sẽ phải sử dụng `"</select>` ở trước

Thử với câu lệnh `"</select><body%20src=1%20onload=alert(1)>`

![image](https://user-images.githubusercontent.com/72268643/151230287-b0cd867b-94ac-450e-8ec4-f78e2938766a.png)
