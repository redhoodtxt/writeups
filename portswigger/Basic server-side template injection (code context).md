*This lab is vulnerable to server-side template injection due to the way it unsafely uses a Tornado template. To solve the lab, review the Tornado documentation to discover how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory.
You can log in to your own account using the following credentials: wiener:peter*

Logged in and chose my preferred name to see this request:
![[Screenshot 2024-06-03 at 10.32.53 AM.png]]
Saw that it controlled the name in the comment section of a blog. I posted a comment and injected the following payload into the change display name request to see if i can break out of the expression and inject code that can be evaluated:
![[Screenshot 2024-06-03 at 11.08.59 AM.png]]
I then injected the following code to delete the file `morale.txt`:
![[Screenshot 2024-06-03 at 11.10.42 AM.png]]
Syntax was found here: [HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#tornado-python)
