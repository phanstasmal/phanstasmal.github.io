---
layout: post
title:  "Cài đặt Apache, MySQL, Php on Ubuntu"
date:   2014-09-17 05:56:00
categories: mysql
---

#####1. Cài đặt Apache:  
Mở terminal gõ command:  
```
~$ sudo apt-get update  
~$ sudo apt-get install apache2
```  

Kiểm tra version cài đặt:  
```
~$ apache2 -v
```  

Kết quả   

> Server version: Apache/2.4.7 (Ubuntu)  
> Server built:   Jul 22 2014 14:36:38  

#####2. Cài đặt MySQL:
Từ terminal gõ command:  
```
~$ sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql
```  
trong quá trính cài đặt mysql-server sẽ hỏi bạn cấu hình password cho user: root, nhập password -> 0k  
Sau khi quá trình cài đặt kết thúc, ta kiểm tra mysql vừa cài đặt:  
```
~$ mysql -hlocalhost -uroot -ppassword 
```  

Với:   

> host là: localhost   
> user là: root  
> password của user là: password (password bạn đặt trong quá trình cấu hình)  

Kết quả: 

> Welcome to the MySQL monitor.  Commands end with ; or \g.  
> Your MySQL connection id is 43  
> Server version: 5.5.38-0ubuntu0.14.04.1 (Ubuntu)  
>   
> Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.  
>   
> Oracle is a registered trademark of Oracle Corporation and/or its  
> affiliates. Other names may be trademarks of their respective  
> owners.  
>   
> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.  
>   
> mysql>  

Từ mysql gõ command:  
```
mysql> show databases;
```  

Kết quả:  

> +--------------------+  
> | Database           |  
> +--------------------+  
> | information_schema |  
> | mysql              |  
> | performance_schema |  
> +--------------------+  
> 3 rows in set (0.00 sec)  

####3. Cài đặt php
Từ terminal gõ command:  
```
~$ sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
```  
Kiểm tra version php5  
```
~$ php5 -v
```  

Kết quả:  

> PHP 5.5.9-1ubuntu4.4 (cli) (built: Sep  4 2014 06:56:34)   
> Copyright (c) 1997-2014 The PHP Group  
> Zend Engine v2.5.0, Copyright (c) 1998-2014 Zend Technologies  
> with Zend OPcache v7.0.3, Copyright (c) 1999-2014, by Zend Technologies   

####4. Cài đặt PHP Module
Từ terminal gõ command:  
```
~$ apt-cache search php5-
```  

Kết quả:  

> php5-cgi - server-side, HTML-embedded scripting language (CGI binary)  
> php5-cli - command-line interpreter for the php5 scripting language  
> php5-common - Common files for packages built from the php5 source  
> php5-curl - CURL module for php5  
> php5-dbg - Debug symbols for PHP5  
> php5-dev - Files for PHP5 module development  
> php5-gd - GD module for php5  
> php5-gmp - GMP module for php5  
> php5-json - JSON module for php5  
> php5-ldap - LDAP module for php5  
> php5-mysql - MySQL module for php5  
> php5-odbc - ODBC module for php5  
> php5-pgsql - PostgreSQL module for php5  
> php5-pspell - pspell module for php5  
> php5-readline - Readline module for php5  
> php5-recode - recode module for php5  
> php5-snmp - SNMP module for php5  
> php5-sqlite - SQLite module for php5  
> php5-tidy - tidy module for php5  
> php5-xmlrpc - XML-RPC module for php5  
> php5-xsl - XSL module for php5  
> libphp5-embed - HTML-embedded scripting language (Embedded SAPI library)  
> php5-adodb - Extension optimising the ADOdb database abstraction library  
> php5-apcu - APC User Cache for PHP 5  
> php5-enchant - Enchant module for php5  
> php5-exactimage - fast image manipulation library (PHP bindings)  
> php5-fpm - server-side, HTML-embedded scripting language (FPM-CGI binary)  
> php5-gdcm - Grassroots DICOM PHP5 bindings  
> php5-gearman - PHP wrapper to libgearman  
> php5-geoip - GeoIP module for php5  
> php5-gnupg - wrapper around the gpgme library  
> php5-imagick - ImageMagick module for php5  
> php5-imap - IMAP module for php5  
> php5-interbase - interbase/firebird module for php5  
> php5-intl - internationalisation module for php5  
> php5-lasso - Library for Liberty Alliance and SAML protocols - PHP 5 bindings  
> php5-librdf - PHP5 language bindings for the Redland RDF library  
> php5-mapscript - php5-cgi module for MapServer  
> php5-mcrypt - MCrypt module for php5  
> php5-memcache - memcache extension module for PHP5  
> php5-memcached - memcached extension module for PHP5, uses libmemcached  
> php5-midgard2 - Midgard2 Content Repository - PHP5 language bindings and module  
> php5-ming - Ming module for php5  
> php5-mongo - MongoDB database driver  
> php5-msgpack - PHP extension for interfacing with MessagePack  
> php5-mysqlnd - MySQL module for php5 (Native Driver)  
> php5-mysqlnd-ms - MySQL replication and load balancing module for PHP  
> php5-oauth - OAuth 1.0 consumer and provider extension  
> php5-pinba - Pinba module for PHP 5  
> php5-ps - ps module for PHP 5  
> php5-radius - PECL radius module for PHP 5  
> php5-redis - PHP extension for interfacing with Redis  
> php5-remctl - PECL module for Kerberos-authenticated command execution  
> php5-rrd - PHP bindings to rrd tool system  
> php5-sasl - Cyrus SASL Extension  
> php5-stomp - Streaming Text Oriented Messaging Protocol (STOMP) client module for PHP 5  
> php5-svn - PHP Bindings for the Subversion Revision control system  
> php5-sybase - Sybase / MS SQL Server module for php5  
> php5-tokyo-tyrant - PHP interface to Tokyo Cabinet's network interface, Tokyo Tyrant  
> php5-vtkgdcm - Grassroots DICOM VTK PHP bindings  
> php5-xcache - Fast, stable PHP opcode cacher  
> php5-xdebug - Xdebug Module for PHP 5  
> php5-xhprof - Hierarchical Profiler for PHP5  

Chọn một trong số các module để cài đặt, cài đặt bằng cách:  
```
~$ sudo apt-get install <tên_module>
```  

Kiểm tra kết quả:  
Tạo file info.php trong `/var/www/` với nội dung:  
```
<?php  
phpinfo();  
?>  
```  
Restart lại server apache2  
```
~$ sudo service apache2 restart  
```  
Mở trình duyệt với `http://127.0.0.1/info.php` xem kết quả.