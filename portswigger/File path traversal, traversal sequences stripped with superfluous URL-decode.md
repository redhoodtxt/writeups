*This lab contains a path traversal vulnerability in the display of product images.
The application blocks input containing path traversal sequences. It then performs a URL-decode of the input before using it.
To solve the lab, retrieve the contents of the /etc/passwd file.*

Used a predefined payload `dotdotpwn.txt` to start and intruder attack on the request to open image in another tab. 
Predefined points is the `filename` parameter value
