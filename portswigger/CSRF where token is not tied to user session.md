*This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't integrated into the site's session handling system.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You have two accounts on the application that you can use to help design your attack. The credentials are as follows:
`wiener:peter`
`carlos:montoya`*

I logged into my account and changed my email, noting that I received a different token for each request:
![[Screenshot 2024-05-23 at 10.51.12 AM.png]]
![[Screenshot 2024-05-23 at 10.52.05 AM.png]]
Delivering a CSRF exploit by reusing a one of the tokens was not possible, so I deduced that reused tokens are not accepted. This was proven when I sent one of the requests to the *Repeater* :
![[Screenshot 2024-05-23 at 10.54.31 AM.png]]
I then decided to intercept a request to change the email, copy the `csrf` token and then drop that request. I then pasted that token into my PoC in the exploit:
![[Screenshot 2024-05-23 at 10.56.35 AM.png]]
I stored the exploit and delivered it to the victim, solving the lab. 
