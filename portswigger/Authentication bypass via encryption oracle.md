*This lab contains a logic flaw that exposes an encryption oracle to users. To solve the lab, exploit this flaw to gain access to the admin panel and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter *

Logged in and noticed that I could stay signed in. Clicked on that and viewed the blog posts as there was nothing else to do. 
I then decided to play around with the parameter of the comment functionality and saw that I get a notification cookie when using a invalid email:
![[Screenshot 2024-05-12 at 11.34.22 PM.png]]
The string for the stay logged in cookie and the notification cookie look similar, so I sent the request with the notification to the *Repeater* and replaced the `notification` cookie with the `stay-logged-in` cookie to observe the behaviour, since whatever in the `notification` cookie gets displayed as an output on the website:
![[Screenshot 2024-05-12 at 11.39.24 PM.png]]

https://infosecwriteups.com/write-up-authentication-bypass-via-encryption-oracle-portswigger-academy-4b4e363347b9