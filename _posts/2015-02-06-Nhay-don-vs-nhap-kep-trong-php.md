---
layout: post
title:  "So sánh nháy đơn và nháy kép trong PHP"
date:   2015-02-06 03:48:00
categories: layout
---

Việc xác định khác biệt giữa dấu nháy đơn `(')` và dấu nháy kép `(")` trong php nó như thế nào?  
	- Dấu nháy đơn `(')`: Chuỗi trong dấu nháy đơn không được phân tích cú pháp, có nghĩa là những gì được viết trong dấu nháy đơn sẽ được xuất hiện. Các ký ký hiệu `\n` (xuống dòng), `\t` (tab) sẽ không được xác định.  
	- Dấu nháy kép `(")`: Chuỗi trong dấu nháy kép được phấn tích cú pháp và bất kỳ biến trong php sẽ được xác định. Các ký ký hiệu `\n` (xuống dòng), `\t` (tab) được xác định.  

Vì chuổi trong dấu nháy kép được phân tích trong quá trình thực thi, theo lý thuyết thì sử dụng dấu nháy đơn sẽ cải thiện hiệu suất vì trong PHP không phải đánh giá chuổi đơn. Điều này đúng với một mô hình nhất định, với ứng dụng trong thực tế nếu ở mức độ trung bình thì sự khác biệt là quá nhỏ nên điều này không thực sự quan trọng. Vì vậy đối với úng dụng trung bình nó không có vấn đề gì để bạn phải lựa chọn. Nếu với ứng dụng tải rất cao thì bạn nên xem xét lựa chọn.  

	- Đọc thêm:  
[http://php.net/manual/en/language.types.string.php](http://php.net/manual/en/language.types.string.php)  
[http://phpbench.com/](http://phpbench.com/)  
[http://stackoverflow.com/questions/13620/speed-difference-in-using-inline-strings-vs-concatenation-in-php5](http://stackoverflow.com/questions/13620/speed-difference-in-using-inline-strings-vs-concatenation-in-php5)  
