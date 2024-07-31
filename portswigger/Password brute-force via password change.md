*This lab's password change functionality makes it vulnerable to brute-force attacks. To solve the lab, use the list of candidate passwords to brute-force Carlos's account and access his "My account" page.
Your credentials: wiener:peter
Victim's username: carlos
Candidate passwords*

Logged into the website with the given credentials and was greeted with the following:
![[Screenshot 2024-05-07 at 3.39.50 PM.png]]
brute-forcing for *carlos*'s current password to change his passwords did not work as it just redirected me to the login page, so I decided to test the error responses when trying to change passwords. 

When supplementing the correct current password and mismatching the new passwords, I came across the following message:
![[Screenshot 2024-05-07 at 3.45.38 PM 2.png]]

Hence, I sent this request to the *Intruder*, set the payload as the current password. I mismatched the passwords and inserted the default wordlist as the payload:
![[Screenshot 2024-05-07 at 3.53.55 PM.png]]
![[Screenshot 2024-05-07 at 3.50.19 PM.png]]
I then added the *Grep Match* rule by copying the password mismatch error and pasting it into it:
![[Screenshot 2024-05-07 at 3.54.53 PM.png]]
This was the result when sorting my the string:
![[Screenshot 2024-05-07 at 3.55.36 PM.png]]
I used the given password to log into *carlos*'s account to complete the lab.

