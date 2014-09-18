---
layout: post
title:  "Nên sử dụng Storage Engine nào InnoDB, MyISAM hay MEMORY khi dùng MySQL"
date:   2014-09-16 10:41:00
categories: mysql
---

InnoDB và MyISAM, khác nhau giữa InnoDB và MyISAM, so sánh InnoDB và MyISAM, dùng InnoDB hay MyISAM, Kiểu table MEMORY trong mySQL

MySQL là hệ quản trị cơ sở dữ liệu miễn phí được sử dụng nhiều nhất khi ứng dụng được viết bằng ngôn ngữ PHP. Tuy nhiên, khi tạo 1 bảng trong MySQL sẽ có nhiều kiểu Storage Engine để bạn lựa chọn. Trong đó có 3 kiểu lưu trữ bảng được dùng nhiều nhất là InnoDB, MyISAM và Memory.

Nhưng ta nên dùng InnoDB,MyISAM hay MEMORY ? Tại sao lại như thế ? Bài viết này sẽ giúp các bạn nắm được cách hoạt động của các Storage Engine này. Từ đó có thể biết được cách chọn loại phù hợp khi xây dựng website của mình để hiệu suất và độ ổn định đạt được cao nhất.

#####1. MyISAM 

Đây là kiểu Storage Engine mặc định khi tạo bảng và được dùng phổ biết nhất. Storage Engine này cho phép lập chỉ mục toàn cột (Full Text Index). Do đó, Storage Engine này cho tốc độ truy suất (Đọc và tìm kiếm) nhanh nhất trong các Storage Engine.

Tuy nhiên, Nhược điểm của MyISAM là hoạt động theo kiểu Table Level locking nên khi cập nhật (Thêm,xóa,sửa) 1 bản ghi nào đó trong cùng 1 table thì table đó sẽ bị khóa lại, không cho cập nhật (Thêm,xóa,sửa) cho đến khi thao tác cập nhật trước đó thực hiện xong.

Ngoài ra, do thiết kế đơn giản và không kiểm tra ràng buộc dữ liệu nên loại Storage Engine này dễ bị hỏng chỉ mục và dễ bị Crash. Đây là cơn ác mộng của các webmaster khi table Crash là table có dung lượng lớn, khi phục hồi rất lâu và hồi hộp

Làm sao để chuyển 1 bảng từ Storage Engine khác (VD: InnoDB) sang MyISAM ?  
Bạn có thể dùng truy vấn sau:  
```ALTER TABLE table_name ENGINE = MyISAM;```

#####2. InnoDB

Đây là kiểu Storage Engine mới hơn MyISAM. Storage Engine này không hỗ trợ Full Text Index như MyISAM (Tin mừng là sắp có hỗ trợ ở các phiên bản mới, hiện tại đã có beta rồi ) nhưng hỗ trợ quan hệ giữa các bảng (Khóa ngoại). Do đó, kiểu Storage này kiểm tra tính toàn vẹn dữ liệu và ràng buộc rất cao => Khó sảy ra tình trạng hỏng chỉ mục và Crash như MyISAM.

Ngoài ra, kiểu Storage Engine này hoạt động theo cơ chế Row Level Locking nên khi cập nhật (Thêm,xóa,sửa) 1 bảng thì chỉ có bản ghi đang bị thao tác bị khóa mà thôi, các hoạt động khác trên table này vẫn diễn ra bình thường.

Vì những tính chất trên, kiểu Storage Engine này thích hợp sử dụng cho Ngân hàng và các trang web có tần suất cập nhật dữ liệu cao như Mạng xã hội, diễn đàn....

Tuy nhiên, nó có nhược điểm là hoạt động tốn RAM hơn so với MyISAM (Nếu MyISAM mà tần suất insert hay update cao thì nếu cấu hình chưa đủ mạnh thì khéo còn tốn RAM nhiều hơn InnoDB vì hàng đợi lớn )

=> vBulletin, mã nguồn diễn đàn lớn nhất hiện nay thật sai lầm khi chọn MyISAM làm kiểu Storage Engine cho các bảng dữ liệu forum. Vì thế mà các trang lớn mới hay bị Crash bảng như vậy (Database Error)

Làm sao để chuyển 1 bảng từ Storage Engine khác (VD: MyISAM) sang InnoDB ?  
Bạn có thể dùng truy vấn sau:  
```ALTER TABLE table_name ENGINE = InnoDB;```  
(Lưu ý là nếu trước đó table này dùng MyISAM mà có cột nào đặt Full Text Index thì bạn phải xóa Full Text Index trên cột đó đi mới có thể chuyển được)


#####3. MEMORY 

Đây là kiểu Storage Engine được lưu trữ dữ liệu trực tiếp lên RAM nên tốc độ truy xuất và cập nhật rất nhanh. Vì thế, nó được dùng làm các table chứa dữ liệu tạm, chứa các phiên làm việc của user...

Khi khởi động lại dịch vụ MySQL thì dữ liệu trên bảng có Storage Engine là MEMORY sẽ mất hết dữ liệu. Chính vì thế nên khi các bạn khởi động lại mysqld trên VPS hay Server thì sẽ thấy số người online = 0  
MEMORY sử dụng cơ chế table-level locking như MyISAM.

Dung lượng của 1 bảng Storage Engine dạng MEMORY tối đa là bao nhiêu ?
Nó phụ thuộc vào cấu hình thông số max_heap_table_size trong file my.cnf, mặc định 1 bảng kiểu MEMORY có dung lượng tối đa là 16MB. Nếu vượt quá bạn sẽ nhận được lỗi: Table xyz is full...

######4. So sánh các đặc điểm của InnoDB vs MyISAM

InnoDB hỗ trợ relationship (data integrity and foreign key constraints) còn MyISAM thì ko: Đa phần các open source đều không coi trọng việc này nhưng nếu ứng dụng của bạn bắt buộc phải dùng foreign key constraints thì InnoDB là lựa chọn của bạn.

InnoDB hỗ trợ transactions còn MyISAM thì không: Nếu hệ thống của bạn dùng trong các ứng dụng ngân hàng hoặc phải thực hiện việc giao dịch thì chắc chắn là MyISAM sẽ bị loại.

Khi nào cần dùng Transaction ?  
Khi ta muốn bảo đảm sự toàn vẹn của dữ liệu (không tạo ra các record mồ côi hoặc chứa thông tin sai lệch).

DùngTransaction để làm gì?  
Để đảm bảo sự toàn vẹn của dữ liệu.

Lợi ích của nó ?  
Lợi ích là đảm bảo sự toàn vẹn của dữ liệu.

Ví dụ như trong ngân hàng bạn còn $150, bạn lên internet, vào 2 trang web cùng 1 lúc, mua 2 món hàng cùng lúc, một món trị giá $50 và 1 món trị giá $20.
Vậy, nếu đúng thì tài khoản của bạn phải còn lại $150 - $50-$20 = $80.

Tuy nhiên, thử tưởng tượng như sau:  
- Đầu tiên ngân hàng nhận được yêu cầu mua hàng từ trang web 1, nó đọc tài khoản của bạn ra giá trị $150.  
- Ngay lúc đó ngân hàng cũng nhận được yêu cầu từ trang web 2, nó đọc tài khoản của bạn, ra giá trị $150.  
- Sau đó, vụ mua bán thứ nhất kết thúc, ngân hàng ghi lại vào tải khoản của bạn là $150-$50 = $100  
- Lúc này vụ mua bán thứ 2 kết thúc và ngân hàng ghi lại vào tải khoản của bạn $150-$20 = $130  
=> vậy là cuối cùng bạn còn $130 (sai) thay vì $80 (đúng).  
Do vậy transaction được dùng để tránh những trường hợp tương tự như trên xảy ra.

InnoDB thiên về row-level locking còn MyISAM thiên về table locking: Tức là khi hệ thống của bạn phải thực hiện nhiều các thao tác insert/update thì InnoDB là tốt hơn, còn nếu hệ thống của bạn thực hiện các thao tác select là chủ yếu thì dùng MyISAM là lựa chọn tốt hơn.

MyISAM hỗ trợ full-text searches còn InnoDB thì không: Đây rõ ràng là một điểm yếu của InnoDB so với MyISAM, và dĩ nhiên là trong hệ thống có dùng full-text searches thì phải loại InnoDB trước.

Cuối cùng nếu bạn là người mới làm về MySQL (cũng như DB nói chung) thì bạn nên dùng MyISAM vì rằng nó đơn giản hơn InnoDB.

#####Tóm lại,
- Với 1 ứng dụng có tần suất đọc cao như trang tin tức,blog... thì bạn nên dùng MyISAM.  
- Với ứng dụng có tần suất insert và update cao như: Diễn đàn, mạng xã hội.. thì bạn nên dùng InnoDB  
- Bạn nên dùng MEMORY Storage Engine cho các table chứa dữ liệu tạm và thông tin phiên làm việc của người dùng (Session)  
- Việc chuyển đổi 1 table từ storage engine này sang storage engine khác sẽ diễn ra tương đối lâu nếu dữ liệu trên table lớn. Do đó cần kiên nhẫn.

------------------------------------------------------------------------------------------------------- 

[a] InnoDB utilies hash indexes internally for its Adaptive Hash Index feature.  
[b] InnoDB support for FULLTEXT indexes is available in MySQL 5.6.4 and higher.  
[c] Compressed MyISAM tables are supported only when using the compressed row format. Tables using the compressed row format with MyISAM are read only.  
[d] Compressed InnoDB tables require the InnoDB Barracuda file format.  
