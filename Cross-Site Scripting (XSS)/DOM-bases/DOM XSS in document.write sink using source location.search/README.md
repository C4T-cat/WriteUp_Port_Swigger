# YÊU CẦU: Gọi hàm `alert()`

# Hướng làm: 

Theo như mô tả của bài thì thanh công cụ search bị gặp lỗi XSS do sử dụng hàm `document.write` để viết dữ liệu in ra màn hình.

Đầu tiên, chúng ta thử nhập 1 chuỗi bất kì vào chỗ tìm kiếm. Kết quả tuy không hiển thị được gì nhưng khi check sourcecode ta có:

![image](https://user-images.githubusercontent.com/72268643/151224395-40a8de08-a932-4ace-a137-02ec59207184.png)

Đây là công cụ tìm kiếm của chúng ta. Từ khóa chúng ta nhập vào sẽ gộp với 1 chuỗi (dấu `""`) để tạo thành 1 URL để tìm kiếm. 

Vậy để XSS được trang web này, ta cần phải thêm `">` để đóng thẻ và chạy câu lệnh bạn muốn thực thi ở sau:

Thử với một vài thẻ như `div`,`img`,`svg` ta đều có thể thực hiện được XSS và hoàn thành lab. 

![image](https://user-images.githubusercontent.com/72268643/151225685-efd4a9cd-3957-4e9b-afe4-1cdb3dc045fc.png)
