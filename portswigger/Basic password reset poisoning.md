*This lab is vulnerable to password reset poisoning. The user carlos will carelessly click on any links in emails that he receives. To solve the lab, log in to Carlos's account.
You can log in to your own account using the following credentials: wiener:peter. Any emails sent to this account can be read via the email client on the exploit server.*

I clicked on the *Forgot password?* link at the homepage. 
I turned *Intercept* and typed in and submitted the username *wiener* into the field for password reset:
![[Screenshot 2024-06-06 at 10.20.06 AM.png]]
I then checked my email client and the request to for password reset:
![[Screenshot 2024-06-06 at 10.22.02 AM.png]]
We see that the same `Host` is used to dynamically generate a password rest link for us. Let's repeat this process, but this time we submit the username *carlos* for the password reset and intercept the `POST` request:
![[Screenshot 2024-06-06 at 10.24.06 AM.png]]
I then changed the `Host` header to that of my exploit server and forwarded the request:
![[Screenshot 2024-06-06 at 10.38.02 AM.png]]
I then checked the access log, where the relative path with the token was seen:
![[Screenshot 2024-06-06 at 10.43.48 AM.png]]
I then copied the token and used it to replace the token in the original URL link to reset password:
![[Screenshot 2024-06-06 at 10.49.58 AM.png]]
I then changed the password and logged in as *carlos*:
![[Screenshot 2024-06-06 at 10.51.22 AM.png]]
