*This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter*

Noticed the following when accessing the website:
![[Screenshot 2024-05-10 at 4.52.18 PM.png]]
Looking at the bottom, we see the following:
![[Screenshot 2024-05-10 at 5.03.10 PM.png]]
I deduced that it required my email, so I updated my email in *My account* and signed up for the newsletter. This gave me the following:
![[Screenshot 2024-05-10 at 5.04.47 PM.png]]
I tried to repeatedly applying the `NEWCUST5` coupon, but was met with the following error:
![[Screenshot 2024-05-10 at 5.06.34 PM.png]]
I then tired to alternate between the `NEWCUST5` coupon and the `SIGNUP30` coupon to see if that was possible. 
This was possible, so I kept repeating this until the price was lower than my store credit:
![[Screenshot 2024-05-10 at 5.08.58 PM.png]]
I then placed my order, solving the lab.