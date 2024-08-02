*This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
You can log in to your own account using the following credentials: wiener:peter*

Logged in and changed my email. Sent the request to the *Repeater* and changed the request method to `GET`. 
Added `&_method=POST` parameter into the URL and observed that the request is sent successfully:
![Screenshot 2024-05-24 at 12.47.51 PM](images/Screenshot%202024-05-24%20at%2012.47.51%20PM.png)
Changing the request method to `GET` will allow it to send the cookie over as it is the correct request and there is a top level navigation for `SameSite=Lax` (the default `SameSite` when the cookie attribute does not appear in the request). Overriding it to `POST` after keeps the cookie while allowing the request to go through. 
I generated the following PoC:
![Screenshot 2024-05-24 at 12.57.12 PM](images/Screenshot%202024-05-24%20at%2012.57.12%20PM.png)
Stored the above in the exploit server and sent it to the victim, solving the lab.
