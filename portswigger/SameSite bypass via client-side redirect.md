*This lab's change email function is vulnerable to CSRF. To solve the lab, perform a CSRF attack that changes the victim's email address. You should use the provided exploit server to host your attack.
You can log in to your own account using the following credentials: wiener:peter*

Noticed that there was `SameSite=Strict` enabled:
![[Screenshot 2024-05-24 at 2.19.02 PM.png]]
When posting a comment on a blog, I found out that you get redirected to the main page afterwards. I could potentially use that redirect as a gadget to bypass the `SameSite=Strict` restriction. 
Sent the request to the *Repeater* and modified it to the following:
![[Screenshot 2024-05-24 at 2.56.55 PM.png]]
This worked, where the redirect sent me back to my account. 
I then tried to see if I could change my email this way:
![[Screenshot 2024-05-24 at 2.58.44 PM.png]]
I had to encode the `submit` parameter so that it parses through. This worked as well, where my email was changed.
I decided to generate a PoC from this:
![[Screenshot 2024-05-24 at 3.02.28 PM.png]]
Stored this in my exploit server and sent it to the victim, solving the lab.
