*This lab's email change functionality is vulnerable to CSRF. It attempts to block CSRF attacks, but only applies defenses to certain types of requests.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter*

Noticed the following request when changing my email:
![Screenshot 2024-05-19 at 11.57.00 AM](images/Screenshot%202024-05-19%20at%2011.57.00%20AM.png)
Generated the following PoC, changing the request method to `GET` and changing the email:
![Screenshot 2024-05-19 at 11.59.41 AM](images/Screenshot%202024-05-19%20at%2011.59.41%20AM.png)
Pasted the HTML to my exploit server, stored the exploit and delivered it to the victim to solve the lab. 
