*This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.
The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain.
To solve the lab, exploit the SQL injection vulnerability to cause a DNS lookup to Burp Collaborator.*

Opened the login page and sent the request from HTTP History to Burp Intruder. 
Added the payload parameters to the injection point:
![Screenshot 2024-05-03 at 10.01.47 AM 1](images/Screenshot%202024-05-03%20at%2010.01.47%20AM%201.png)
Right clicked to 'scan defined insertion points' as seen below: 
![Screenshot 2024-05-03 at 10.08.20 AM](images/Screenshot%202024-05-03%20at%2010.08.20%20AM.png)
After the scan was finished, I received the following under Target, where a SQL injection vulnerability was detected and the following request with the respective payload was made:
![Screenshot 2024-05-03 at 10.15.38 AM](images/Screenshot%202024-05-03%20at%2010.15.38%20AM.png)
This was the response: 
```Burp 
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 6156
```
And this was the interaction with the Collaborator:
![Screenshot 2024-05-03 at 10.17.46 AM](images/Screenshot%202024-05-03%20at%2010.17.46%20AM.png)

Done!