*This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed using a classic obfuscation technique.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter*

Logged in with my credentials and uploaded a malicious script that obfuscated the file extension
`exploit.php%00.jpg`
Checked the `GET` request to retrieve the secret:
![Screenshot 2024-05-13 at 2.45.02 PM](images/Screenshot%202024-05-13%20at%202.45.02%20PM.png)
