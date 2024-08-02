*This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. To solve the lab, log in to Carlos's account. You can log in to your own account using the following credentials: wiener:peter. Any emails sent to this account can be read via the email client on the exploit server.*

Sent the forgot password request to the repeater:

![Screenshot 2024-05-07 at 2.16.53 PM](images/Screenshot%202024-05-07%20at%202.16.53%20PM.png)
Edited the request to send it to *carlos* instead and forward his clicking of the link to my exploit server:

![Screenshot 2024-05-07 at 2.17.28 PM 1](images/Screenshot%202024-05-07%20at%202.17.28%20PM%201.png)
His `GET` request appeared under my *Access Logs* in the exploit server, where I found his token. I copied his token and pasted it into my password reset link URL.
![Screenshot 2024-05-07 at 2.18.09 PM 2](images/Screenshot%202024-05-07%20at%202.18.09%20PM%202.png)
After generating the page from that request, I reset the password and then logged into *carlos*'s account with the new credentials:
![Screenshot 2024-05-07 at 2.18.35 PM](images/Screenshot%202024-05-07%20at%202.18.35%20PM.png)