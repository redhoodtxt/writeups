*This lab's two-factor authentication is vulnerable due to its flawed logic. To solve the lab, access Carlos's account page.
Your credentials: wiener:peter
Victim's username: carlos
You also have access to the email server to receive your 2FA verification code.*

Logged in with the given credentials, only to be greeted by a verification page : 
![Screenshot 2024-05-06 at 4.26.29 PM](images/Screenshot%202024-05-06%20at%204.26.29%20PM.png)
I went to my email client to receive my verification code for *wiener*: 
![Screenshot 2024-05-06 at 4.27.43 PM](images/Screenshot%202024-05-06%20at%204.27.43%20PM.png)
%%Lab timed out, so the verification code changed%%

I intercepted the submission my verification code, changed the `verify` value to *carlos*, and sent it to intruder to brute-force the verification code as I had no access to *carlos*'s email:

![Screenshot 2024-05-06 at 4.51.15 PM](images/Screenshot%202024-05-06%20at%204.51.15%20PM.png)
![Screenshot 2024-05-06 at 4.51.36 PM](images/Screenshot%202024-05-06%20at%204.51.36%20PM.png)
This gave the following results, where there was a 302 status for the code `1577`:
![Screenshot 2024-05-06 at 4.53.41 PM](images/Screenshot%202024-05-06%20at%204.53.41%20PM.png)
Sent the submission for the user *carlos* with code 1577 to login successfully: 
![Screenshot 2024-05-06 at 4.54.33 PM](images/Screenshot%202024-05-06%20at%204.54.33%20PM.png)