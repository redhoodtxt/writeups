*This lab contains a path traversal vulnerability in the display of product images.
The application validates that the supplied filename ends with the expected file extension.
To solve the lab, retrieve the contents of the /etc/passwd file.*

Clicked on a product and opened the image in a new tab. I then checked my HTTP history:
![[Screenshot 2024-05-07 at 6.43.57 PM.png]]
Using the predefined payload list `dotdotpwn.txt` and adding the suffix `%00.jpg`(null byte) to each payload via *Payload Processing* setting in *Intruder* (since the parameter required a file extension), I ran the results to get the contents of the passwd file in the results:
![[Screenshot 2024-05-07 at 6.46.02 PM.png]]