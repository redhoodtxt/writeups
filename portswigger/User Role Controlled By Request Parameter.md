*This lab has an admin panel at /admin, which identifies administrators using a forgeable cookie. Solve the lab by accessing the admin panel and using it to delete the user carlos. You can log in to your own account using the following credentials: wiener:peter*

Logged into my account using the given credentials and intercepted the request using Burp Intercept: 

I noticed that the admin was set to `false` when logging in:
```Burp 
GET /login HTTP/2
Host: 0a27006203d85c9085d771be00a50013.web-security-academy.net
Cookie: session=nOKlBod9Hfa7eyUG35vKf63NGK9AR2SS; Admin=false
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a27006203d85c9085d771be00a50013.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```
Hence, with each forwarding of request, i changed the admin value to `true`.
![[user role controlled by request params.png]]
I was then able to delete the user *carlos*. 

Done!