*This lab contains a path traversal vulnerability in the display of product images.
The application blocks traversal sequences but treats the supplied filename as being relative to a default working directory.
To solve the lab, retrieve the contents of the /etc/passwd file.*

I clicked on a product and viewed the image in another tab, checking *HTTP History*:
![Screenshot 2024-05-07 at 4.46.23 PM](images/Screenshot%202024-05-07%20at%204.46.23%20PM.png)
I sent the request to the *Repeater* and changed the path in the header to `/etc/passswd`, which output the contents of the passwd file: 
![Screenshot 2024-05-07 at 4.53.54 PM](images/Screenshot%202024-05-07%20at%204.53.54%20PM.png)
