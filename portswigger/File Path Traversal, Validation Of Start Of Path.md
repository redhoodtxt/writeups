*This lab contains a path traversal vulnerability in the display of product images.
The application transmits the full file path via a request parameter, and validates that the supplied path starts with the expected folder.
To solve the lab, retrieve the contents of the /etc/passwd file.*

After opening an image in a new tab, I sent the request to *Intruder*, used the predefined payload `dotdotpwn.txt` and added a prefix of `/var/www/images/` as a rule. 

Running the attack will result in the output of the `/etc/passwd` file. 
