*This lab is subtly vulnerable to username enumeration and password brute-force attacks. It has an account with a predictable username and password, which can be found in the following wordlists:
Candidate usernames
Candidate passwords
To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.*

At the login page, I typed in wrong credentials. This gave a unclear error message as shown: 
![[Screenshot 2024-05-03 at 2.06.41 PM.png]]
The failed login created a request I can observe in Burp's *HTTP History*:
![[Screenshot 2024-05-03 at 2.07.49 PM.png]]
I sent the Request into *Intruder* to brute-force a valid username first. I set the type to *Sniper*, set the defined points at the values of `username=` and uploaded the username wordlist to the payload set, as shown below: 
```Intruder
POST /login HTTP/2
...
username=§wiener§&password=peter
```
![[Screenshot 2024-05-03 at 2.12.01 PM.png]]
I went to settings and set the *Grep-Match* setting to add the string 'Invalid username or password.' This would return 1 if the string was found, or 0, which would mean that the username is correct. 
I sorted the string from ascending order to obtain the following results: 
![[Screenshot 2024-05-03 at 2.36.35 PM.png]]

The username *accounts* does not return the same string value as the rest of the usernames as the string is missing an period. This means that this username is correct. 
We now need to find the correct password for this username. 
I repeated the same process in *Intruder*, as such: 
```Intruder
POST /login HTTP/2
...
username=accounts&password=§peter§
```
![[Screenshot 2024-05-03 at 2.40.14 PM.png]]
I replaced the string to 'Invalid username or password', without the `.` and ran the attack,  sorting the results from ascending: 
![[Screenshot 2024-05-03 at 2.44.02 PM.png]]
The password *shadow* not only failed to return the string, but also had a different status code from the rest of the responses.

 I logged in with the credentials: 
 ![[Screenshot 2024-05-03 at 2.45.48 PM.png]]
Done!