---
layout: post
title:  "Hướng dẫn cài đặt Laravel 4 trên windows"
date:   2014-10-13 10:41:00
categories: jekyll update
---

##Yêu cầu hệ thống:
-	PHP >= 5.4
-	MCrypt PHP Extension

##Cài đặt Web Server xampp:
-	Ở đây mình sử dụng gói xampp Download Xampp for Windows
	Link: https://www.apachefriends.org/index.html
Sau khi cài đặt xampp, start 2 module Apache và MySQL
[Imgur](http://i.imgur.com/siJNvJU)

##Cài đặt laravel:
Cài đặt laravel từ composer
-	Download composer tại địa chỉ: https://getcomposer.org/download/
-	Sau khi download về ta tiến hành cài đặt composer
![alt text](http://i.imgur.com/SjKBz8W)
Click Next,
![alt text](http://i.imgur.com/lq0UcLF)
Chọn Install Shell Menus, Click Next
![alt text](http://i.imgur.com/7Y8Xc7u)
Chọn đường dẫn tới php.exe, ở đây mình sử dụng xampp và cài đặt xam ở ổ D:\ nên có đường dẫn là: `D:\xampp\php\php.exe`, click Next
![alt text](http://i.imgur.com/oy4xEXO)
Click Install, OK
![alt text](http://i.imgur.com/P8XSsBJ)
Sau khi cài đặt xong composer, ta vào thư mục `D:\xampp\htdocs`
Right Click, chọn User Composer here
![alt text](http://i.imgur.com/CNUCz8B)
Xuất hiện cửa sổ cmd ta gõ lệnh
`composer create-project laravel/laravel lrvexample --prefer-dist`
với lrvexample là tên project của bạn.
![alt text](http://i.imgur.com/M0Tea9P)
Enter, đợi quá trình download và cài đặt
![alt text](http://i.imgur.com/sake8a6)
…
(waiting …)
![alt text](http://i.imgur.com/88NYhNo)
Hoàn thành cài đặt laravel.
Thư mục project lrvexample đã được tạo trong xmapp/htdocs
![alt text](http://i.imgur.com/FyA1JPS)

Truy cập địa chỉ để xem kết quả:
`http://localhost:8080/lrvexample/public/`
(8080) là port mình cấu hình để chạy Appache
Mặc định sẽ là :
`http://localhost/lrvexample/public/`
![alt text](http://i.imgur.com/frKRHvH)


