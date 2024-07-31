*This lab is vulnerable due to a logic flaw in its password brute-force protection. To solve the lab, brute-force the victim's password, then log in and access their account page.
Your credentials: wiener:peter
Victim's username: carlos
Candidate passwords

Reaching the login page, I tried checking the errors to see if there were any verbose error messages. 
1. A valid username but incorrect password : 'Incorrect Password'
2. An invalid username but valid password : 'Incorrect username'
3. An incorrect password and username : 'Invalid username'
From the first 3 messages, we can deduce that the application checks the username first to see if it is in the database before checking the password. 
I did a 4th attempt of invalid credentials to see if there will be any blocks to the IP, and received the following message: 

![[Screenshot 2024-05-06 at 9.17.15 AM.png]]
After waiting for a minute, I repeated the the above process, making sure to input the valid credentials on the 3rd attempt to see if the application resets the IP block. This hypothesis proved to be true. 

Given this information, we can create a python script to brute-force the credentials, where we enumerate the password with incorrect credentials every 2 attempts, with 1 correct attempt in between to reset the IP block.

This was the code i used :
```python 
# # generate the wordlist for the username
for i in range(99):
    if(i%3==0):
        print("wiener")
    else:
        print("carlos")

#generate the wordlist for passwords
with open('auth_pw.txt','r') as passwords:
    lines = passwords.readlines()
    
i = 0

for pwd in lines:
    if(i%3==0):
        print("peter")
        
    else:
        print(f"{pwd.strip()}")
    i += 1
```

I then sent the request at login to *Intruder* and:
1. set the mode to pitchfork
2. made the defined payload points as username and password values:
	![[Screenshot 2024-05-06 at 9.51.10 AM.png]]
3. Ran the script and copied the username list into payload 1 and the password list to payload 2:
	![[Screenshot 2024-05-06 at 10.19.40 AM 1.png]]
	
	![[Screenshot 2024-05-06 at 10.20.00 AM 1.png]]
4. set the *Resource Pool* to 1 instead of 10

After running the attack and sorting the results by username *carlos* and status code 302, I got the following: 
![[Screenshot 2024-05-06 at 10.47.54 AM.png]]

Solved!