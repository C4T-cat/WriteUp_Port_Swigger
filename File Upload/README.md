# File Upload

### 1) File Upload là gì ❓
Lỗ hổng này xảy ra khi một hệ thống ứng dụng web không có các quy định nghiêm ngặt về định dạng file được upload lên phía server. Qua đó, chúng ta có thể gửi các file, các phần mềm độc hại và chạy quyền thực thi của hệ thống bên server.

### 2) Phát hiện File Upload 🔎
Để phát hiện được lỗ hổng này chúng ta cần chú ý tới 2 yếu tố:
  - Màng lọc của trang web với các tệp khi được tải lên -> không cho phép up file thực thi
  - Những quyền và hạn chế của file khi ở trên hệ thống lưu trữ phía server -> không cho phép thực thi các file đó

### 3) Khai thác File Upload ⚔
Như đã đề cập ở trên, file upload chỉ là 1 lỗ hổng khá cơ bản và dễ hiểu. Tuy nhiên chúng lại mở đường cho các cách tấn công khác vào server.
![image](https://user-images.githubusercontent.com/72268643/158020257-7f0f9db3-7475-439d-ab64-bea04cb4987d.png)

#### 3.1) Chiếm quyền thực thi từ xa
  - Đây là một cách tấn công phổ biến nhất mà các hacker hay khai thác. Chúng ta có thể liệt kê các tập lệnh cũng như truy cập vào các thông tin nhạy cảm.

#### 3.2) Path Traversal Attack
  - Khi upload file, server sẽ để một chỗ riêng để lưu các file đó. Tuy nhiên chúng ta có thể truy cập các file khác bằng cách đổi tên file thành đường dẫn để tới vị trí mà ta muốn.
  `....path=/folder/test/&filename=../../../test.png`
  - Tuy nhiên, việc ghi đè tệp của hệ thống sẽ khiến cho lỗ hổng này trở nên nguy hiểm hơn.

#### 3.3) DoS, tiêu thụ tài nguyên bằng file kích thước lớn
  - Việc tấn công này được thực hiện bằng việc gửi các file với kích thước lớn (đối với ảnh thì dùng kỹ thuật tấn công Pixel Flood Attack) khiến cho ứng dụng web phản hồi chậm dẫn đến từ chối dịch vụ.

#### 3.4) XSS/SQLi bằng tên ảnh
  - Để thực hiện tấn công XSS/SQLi ta có thể đổi tên ảnh thành 1 câu lệnh thực thi rồi kết thúc đằng đuôi file như:

    - XSS: `<script>alert(document.domain)</script>.png`
    
    - SQLi: `sleep(10)-- -.png`
    
    Rồi sau đó hướng đến vị trí của tệp và xem các phản ứng của ứng dụng web.

#### 3.5) SSRF
  - SSRF là một lỗi khá là khác bởi chúng ta có nhiều cách thực thi lỗi này ngoài việc gọi đến điểm lưu trữ của file đã được up lên. Ngoài ra cũng có khả năng upload file bằng URL cũng như sử dụng các file HTML hoặc SVG để thực thi các lệnh độc hại.

#### 3.6) SVG injection
  - CSV Injection / Formulas Injection / CSV Excel Macro injection là một lỗ hổng thường thấy trong chức năng “Export” thay vì chức năng “Upload”. Nếu tệp tin này không được lọc ở đầu vào thì sẽ chưa được thực thi luôn mà phải đợi đến khi người dùng hệ thống “Export” thì mới có thể thực thi.

#### 3.7) Bypass các bước lọc đầu vào
  - Bypass check đuôi file bằng: Sử dụng các kí tự đặc biệt ở cuối như Null Byte (% 00), %0d, %0a, -> Bypass blacklist: không cho phép php
	  `file.php%20` / `file.php%0a` / `file.php%00` / `file.php%0d%0a` / `file.php/` / `file.php.\` / `file.`
    
    ![image](https://user-images.githubusercontent.com/72268643/158023017-1c835c62-ecce-4a43-bb58-96f0f8d1fb37.png)

  * Ví dụ:  
    - Khi upload, nếu tên file là test.php%20 -> hệ thống hiểu là up file test.php%20
    - Khi thực thi, máy sẽ hiểu là thực thi file test.php’ ‘ -> thực thi thành công

  - Sử dụng nhiều đuôi file -> bypass whitelist: giới hạn đuôi file được up lên: png, jpg -> test.php.png-/-test.php%00.png
  ```
      $target_dir = "uploads/";
      $target_file = $target_dir . basename($_FILES["fileToUpload"]["name"]);
      $uploadOk = 1;
      $splitName = explode(".", $_FILES["fileToUpload"]["name"]);
      $imageFileType = end($splitName);
      $imageFileType = (pathinfo($target_file,PATHINFO_EXTENSION));
  ```
  - Thay đổi content-type (loại file) được phép upload qua các request
    ![image](https://user-images.githubusercontent.com/72268643/158022784-6ad01026-3dc2-4ba1-acaa-cce78ee0b8f2.png)
    ```
     $allowed_type = array('image/gif', 'image/png', 'image/jpg', 'image/jpeg');
      $ctname = $_FILES["fileToUpload"]["type"];
      if (!in_array($ctname, $allowed_type))  {
          echo "Sorry, only JPG, JPEG, PNG & GIF files are allowed. (Check Content-Type). <br>"  ;
          $uploadOk = 0;
      }
    ```
    
    
### 4) Ngăn chặn File Upload 🛡
- Để ngăn chặn việc tấn công bằng file upload thì chắc chắn chúng ta phải nắm rõ được các dạng file chúng ta tải lên, qua đó tạo các blacklist, whitelist đầy đủ.
- Giới hạn dữ liệu file tải lên để ngăn ngừa tấn công DoS.
- Mã hóa các tên file khi người dùng tải lên nhằm tránh việc thực hiện các câu lệnh XSS/SQLi/… cũng như người dùng có thể tìm thấy vị trí file cũng như chống lại việc sử dụng nhiều đuôi file để bypass.
- Sử dụng bản PHP (>=5) mới nhất để có thể loại bỏ các ký tự Null Byte.
- Đảm bảo các tệp tải lên không có quyền thực thi khi được tải lên.
- Sử dụng các phần mềm quét virus định kì để loại bỏ các file độc hại
- Cách ly thư mục lưu file được upload với các thư mục còn lại của hệ thống.
- Nếu nó là máy chủ apache thì thêm cấu hình apache core vào file `conf` để giới hạn filename, có bao gồm cả file extension (jpg, png,...)
  ```
	<FilesMatch ".+\.ph(p[345]?|t|tml)$">
		SetHandler application/x-httpd-php
	</FilesMatch>
   ```

### 5) Writeup các lab trên PortSwigger

| Tình trạng | Tên |
|:-:|-|
| ✔ | [Lab 1: ]() |
| ❌ | [Lab 2: ]() |
| ❌ | [Lab 3: ]() |
| ❌ | [Lab 4: ]() |
| ❌ | [Lab 5: ]() |
| ❌ | [Lab 6: ]() |
| ❌ | [Lab 7: ]() |
| ❌ | [Lab 8: ]() |
| ❌ | [Lab 9: ]() |
| ❌ | [Lab 10: ]() |
| 📁 | []() |
