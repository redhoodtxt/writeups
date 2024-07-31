*This lab contains a vulnerable image upload function. The server is configured to prevent execution of user-supplied files, but this restriction can be bypassed by exploiting a secondary vulnerability.
To solve the lab, upload a basic PHP web shell and use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter *

Logged in with my credentials and noticed that I could upload an avatar image:
![[Screenshot 2024-05-13 at 12.14.32 PM.png]]
I tried uploading a normal image first to observe the response:
![[Screenshot 2024-05-13 at 12.17.06 PM.png]]
I then tried uploading a malicious script to see how the application will respond:"
```
┌──(roshan㉿roshan)-[~/BSCP/file_upload]
└─$ cat exploit.php       
<?php echo file_get_contents('/home/carlos/secret'); ?>
```
This was the result:
![[Screenshot 2024-05-13 at 12.23.36 PM.png]]
The application accepts `.php` scripts, but does not execute the file, returning it as plaintext:
![[Screenshot 2024-05-13 at 12.24.41 PM.png]]
I noticed that once I uploaded the file, there was a filename parameter in the `POST` request:
![[Screenshot 2024-05-13 at 12.44.19 PM.png]]
I sent this request to *Repeater* and attempted a directory traversal, URL-encoding the `/` of the payload :
![[Screenshot 2024-05-13 at 12.59.54 PM.png]]
As seen from above, the payload was successfully uploaded. This means that I can access the `files/exploit.php` page to reveal the secret of *carlos*. I sent the `GET /files/avatars..%2f/exploit.php` to *Repeater* and modified the request as such:
`GET /files/exploit.php`
This gave me the secret:
![[Screenshot 2024-05-13 at 1.03.25 PM.png]]
