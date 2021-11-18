# Lab 1: Determining the number of columns returned by the query

## Yêu cầu 
  Xác định số cột được trả về bởi query bằng SQLi UNION

## Writeup
Chúng ta có 2 cách để xác định số cột:
  
### Cách 1: Sử dụng 'UNION select NULL--

Sau khi vào trang web, chúng ta sử dụng Burp Suit để chặn request khi chọn một thư lục bất kì trên trang web. 
![image](https://user-images.githubusercontent.com/72268643/141676724-b888ce58-fdff-4f3b-9f98-9adb3f6155eb.png)
    
Sau đó gửi request đến Repeater, chúng ta thay đổi giá trị truyền vào category thành **'UNION select NULL--** rồi Sent. 
 ![image](https://user-images.githubusercontent.com/72268643/141677691-3c39a161-2dbe-4bbd-81d6-96fa7e8db870.png)

**Lưu ý: Khi truyền vào cần thay ' ' thành '+' 

Ta thấy Internal Server Error do chưa truyền đúng số cột.
    
Tiếp tục thử lại bằng cách tăng số cột nhập vào: **'UNION select NULL, NULL, NULL--** t thấy Respone đã trả về kết quả.
![image](https://user-images.githubusercontent.com/72268643/141677064-988aefe2-d35c-4152-ae8c-bd565799c9ab.png)
    
=> Hoàn thành lab  
![image](https://user-images.githubusercontent.com/72268643/141677446-b11a0f6f-46ee-4bff-9098-32ba1ff84edb.png)

### Cách 2: Sử dụng 'ORDER BY number--
  
Truyền vào trong category 'ORDER BY 1-- để xem web có đúng 1 cột dữ liệu không. Nếu không thì tiếp tực thử lại và tăng số lượng cho đến khi bị lỗi .
![image](https://user-images.githubusercontent.com/72268643/141677291-0bf0022d-2c0b-4b84-b6cb-a2650d15f943.png)

Khi thử với 4, t thấy trang web bị lỗi => số cột sẽ là 3 => ***DONE***
![image](https://user-images.githubusercontent.com/72268643/141677311-d24ad497-cf2a-4201-a039-b3dc5bdd503e.png)
  
  


    

