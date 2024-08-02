*This lab is vulnerable to username enumeration using its response times. To solve the lab, enumerate a valid username, brute-force this user's password, then access their account page.
Your credentials: wiener:peter
Candidate usernames
Candidate passwords*

Logged into my account with the given credentials and checked *HTTP History*: 
![Screenshot 2024-05-03 at 3.10.20 PM](images/Screenshot%202024-05-03%20at%203.10.20%20PM.png)

I tried a few approaches to logging in on the web page: 
	1. username *wiener* with a password *peter* gave me no errors and a status code of 302
	2. username *wiener* with a wrong password gave me the error 'Invalid username or password.' and the status code 200
	3. invalid username and invalid password gave me the error 'Invalid username or password.' and the status code 200
As the error messages for both 2 and 3 are the same, I cannot obtain a valid username by distinguishing the error messages or the status codes. 
Hence, I decided to check the response timings when doing a brute-force. Ideally, if the a wrong username and a very long password is provided, the response time should be short as the application only needs to verify that the username is in the database. However, if the username is correct but the password is absurdly long and wrong, then the response time would be much longer. 

I decided to try this attack in *Intruder* where I modified the login request to the following: 
```Intruder
POST /login HTTP/2
...
username=§§&password=very-long-strings-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-string-so-very-long-strings@dontwannacry.com.exploit-0afe007b03a34169c10b8fc501510091.exploit-server.net
```
I then uploaded the default users wordlist into the payload set and ran the *Sniper* attack, and was met with the following: 
![Screenshot 2024-05-03 at 3.54.38 PM](images/Screenshot%202024-05-03%20at%203.54.38%20PM.png)
This suggests that there is a ban on my IP for 30 mins due to the brute-force attack creating too many login attempts. I bypassed this by modifying my payload to the following:
1. including the `X-Forwarded-For: 12.13.14.15` header to the request
2. using the *Pitchfork* attack, where I increment the value of `15` in the above IP by 1 each time till 256, and changing the value of the username for each IP used
I added the users wordlist and started the attack. This was the result, when I sorted the response time by descending: 

![Screenshot 2024-05-03 at 4.06.12 PM](images/Screenshot%202024-05-03%20at%204.06.12%20PM.png)
The username *asia* has the longest and most stark response time, so I'll brute-force the password with this username using *Sniper* and the relevant password wordlist. This was the result: 

![Screenshot 2024-05-03 at 4.23.41 PM](images/Screenshot%202024-05-03%20at%204.23.41%20PM.png)
As the above, credentials give the 302 status, we can send it to the *Repeater*, send the request and solve the lab!

