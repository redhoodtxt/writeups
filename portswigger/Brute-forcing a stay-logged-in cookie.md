*This lab allows users to stay logged in even after they close their browser session. The cookie used to provide this functionality is vulnerable to brute-forcing.
To solve the lab, brute-force Carlos's cookie to gain access to his "My account" page.
Your credentials: wiener:peter
Victim's username: carlos
Candidate passwords*

Logged in with the given credentials, checking in the stay logged in checkbox and checked *HTTP History*. I found the cookie that keeps the logged in token in the request below, and decoded it using *Inspector*:
![Screenshot 2024-05-06 at 5.38.44 PM](images/Screenshot%202024-05-06%20at%205.38.44%20PM.png)
The random string of characters concatenated to *wiener* in the token looks like a hash value, so I used CrackStation to see if it could be a hash. As seen from the result below, it is a MD5 hash of the password for *wiener*. 
![Screenshot 2024-05-06 at 5.40.39 PM](images/Screenshot%202024-05-06%20at%205.40.39%20PM.png)

I tried testing if there was any protection against brute-forcing. After making 3 invalid attempts, you are unable to log in for a minute, as seen below:
![Screenshot 2024-05-07 at 9.21.08 AM](images/Screenshot%202024-05-07%20at%209.21.08%20AM.png)

Hence, I then tried to check if alternating between a valid and invalid attempt would reset the counter on the block. This gave the same error message as above. Hence, I decided to:
1. create the following script to hash the password in MD5 and append the username *carlos* as a prefix
```python
#generate the wordlist for passwords
import hashlib
# String to be encoded
string_to_encode = "Hello, world!"
# Create an MD5 hash object
md5_hash = hashlib.md5()

passwd = "peter"
passwd = md5_hash.update(passwd.encode('utf-8'))
passwd = encoded_string = md5_hash.hexdigest()

new = open("stay_logged_in.txt","w+")
with open('auth_pw.txt','r') as passwords:
    lines = passwords.readlines()
    for line in lines: 
        # Update the hash object with the string's bytes
        line = md5_hash.update(line.encode('utf-8'))
        # Get the hexadecimal representation of the hash
        line = encoded_string = md5_hash.hexdigest() 
        new.write(f"carlos:{line}\n")
        # new.write(f"wiener:{passwd}\n")
passwords.close

new.close


```
2. Start an *Intruder* attack, setting the predefined point as the `stay-logged-in` cookie value and changing the `id` to *carlos*:
	- Note** : remember to remove the session cookie
![Screenshot 2024-05-07 at 9.33.22 AM](images/Screenshot%202024-05-07%20at%209.33.22%20AM.png)
3. Under *Payloads*, I used the *Payloads Processing* setting to encode each payload in base64:
![Screenshot 2024-05-07 at 9.35.32 AM](images/Screenshot%202024-05-07%20at%209.35.32%20AM.png)
4. I then went under *Resource Pool* and modified the settings such that the number of concurrent requests is 3 and the delay between requests is 1+ min.
This gave the following results, completing the lab!
![Screenshot 2024-05-07 at 9.54.00 AM](images/Screenshot%202024-05-07%20at%209.54.00%20AM.png)
