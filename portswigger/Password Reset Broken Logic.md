*This lab's password reset functionality is vulnerable. To solve the lab, reset Carlos's password then log in and access his "My account" page.
Your credentials: wiener:peter
Victim's username: carlos*

Logged in with the given credentials, took note of my email and logged out. 

Clicked on *Forgot Password?* at the login page, submitted my email, clicked on the link in the email client and viewed the request in *HTTP History*.
![Screenshot 2024-05-07 at 11.30.58 AM](images/Screenshot%202024-05-07%20at%2011.30.58%20AM.png)
Notice a token was generated when clicking on the link given in the email client for resetting password.

I decided to change my password and submit the request to see if there was a request with both by credentials and the token after submission, and indeed there was:
![Screenshot 2024-05-07 at 11.34.22 AM](images/Screenshot%202024-05-07%20at%2011.34.22%20AM.png)
Modified the username to *carlos* and sent it to the repeater, which gave back a 302 status code:
![Screenshot 2024-05-07 at 11.37.16 AM](images/Screenshot%202024-05-07%20at%2011.37.16%20AM.png)
Logged in with the new password and *carlos* as the username to complete the lab:
![Screenshot 2024-05-07 at 11.38.24 AM](images/Screenshot%202024-05-07%20at%2011.38.24%20AM.png)
