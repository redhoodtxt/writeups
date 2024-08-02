*This lab's email change functionality is vulnerable to CSRF.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You can log in to your own account using the following credentials: wiener:peter*

Noticed the following request when changing my email:
![Screenshot 2024-05-23 at 10.17.20 AM](images/Screenshot%202024-05-23%20at%2010.17.20%20AM.png)
I created a CSRF PoC, removing the `csrf` parameter and changing the email:
![Screenshot 2024-05-23 at 10.20.42 AM](images/Screenshot%202024-05-23%20at%2010.20.42%20AM.png)
I pasted this into my exploit server, stored it and delivered it to the victim to solve the lab.
