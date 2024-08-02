*This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.The SQL query is executed asynchronously and has no effect on the application's response. However, you can trigger out-of-band interactions with an external domain. The database contains a different table called users, with columns called username and password. You need to exploit the blind SQL injection vulnerability to find out the password of the administrator user.*
*To solve the lab, log in as the administrator user.* 

Accessed the login page and checked HTTP History: 
![Screenshot 2024-05-03 at 11.28.34 AM](images/Screenshot%202024-05-03%20at%2011.28.34%20AM.png)

I then sent this request to Intruder, added defined the payload insertion points and scanned it as follows: 
![Screenshot 2024-05-03 at 11.28.02 AM](images/Screenshot%202024-05-03%20at%2011.28.02%20AM.png)

After the scan was complete, I received the following results under Dashboard, where there was a OAST vulnerability based on the payload used:
![Screenshot 2024-05-03 at 11.26.31 AM](images/Screenshot%202024-05-03%20at%2011.26.31%20AM.png)
I sent the request that the scan used to Repeater, modifying the DNS link used to that of under Collaborator (Copy to Clipboard function) and inserted a SQL query to extract the password and append it to the subdomain, all using the Inspector function: 
![Screenshot 2024-05-03 at 11.25.11 AM](images/Screenshot%202024-05-03%20at%2011.25.11%20AM.png)
Checking under Collaborator, we see the password appended to the subdomain: 

![Screenshot 2024-05-03 at 11.24.39 AM](images/Screenshot%202024-05-03%20at%2011.24.39%20AM.png)

Using this password, I logged in as *Administrator*: 
![Screenshot 2024-05-03 at 11.23.57 AM 1](images/Screenshot%202024-05-03%20at%2011.23.57%20AM%201.png)