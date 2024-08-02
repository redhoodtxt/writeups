*This lab is vulnerable to username enumeration. It uses account locking, but this contains a logic flaw. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.
Candidate usernames
Candidate passwords*

I tried username enumeration by observing the error message when logging in with invalid credentials, but was met with a standard error message: 
![Screenshot 2024-05-06 at 11.06.53 AM](images/Screenshot%202024-05-06%20at%2011.06.53%20AM.png)
I decided to create an attack such that I trigger an account lock attempt, which will enumerate a valid username. 

I used *Intruder* to : 
1. set the attack type to *Cluster Bomb*
2. set 2 defined points, 1 for username value, 1 for password value
3. input the respective payloads
![Screenshot 2024-05-06 at 3.55.34 PM](images/Screenshot%202024-05-06%20at%203.55.34%20PM.png)

A valid username *americas* is present. We can now try to enumerate the correct password. 

I tried to check the number of login attempts i had to make before getting locked out the system manually and found that I could only have a maximum of 3 times before I get locked out. 
![Screenshot 2024-05-06 at 4.00.03 PM](images/Screenshot%202024-05-06%20at%204.00.03%20PM.png)
The response shows *My Account*, indicating that we were able to log in successfully without any error!

