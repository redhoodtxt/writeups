*This lab contains a vulnerable image upload function. Certain file extensions are blacklisted, but this defense can be bypassed due to a fundamental flaw in the configuration of this blacklist.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter *

Logged in via my credentials. I wanted to check if the file extension of my exploit file has been blacklisted and if so, the configuration file's location. 
![Screenshot 2024-05-13 at 1.27.43 PM](images/Screenshot%202024-05-13%20at%201.27.43%20PM.png)
Checking the request, I see the following:
![Screenshot 2024-05-13 at 1.31.19 PM](images/Screenshot%202024-05-13%20at%201.31.19%20PM.png)
I decided to upload my own `.htaccess` file to `files/avatars` directory so as to allow `.php5` extensions and then upload my own `exploit.php5` to the same directory. 
This is my `.htaccess` file:
```
┌──(roshan㉿roshan)-[~/BSCP/file_upload]
└─$ cat .htaccess   

AddType application/x-httpd-php .php5
```
After uploading, I received the confirmation as shown below:
![Screenshot 2024-05-13 at 2.26.06 PM](images/Screenshot%202024-05-13%20at%202.26.06%20PM.png)
I then uploaded my `exploit.php5` file to the same directory:
![Screenshot 2024-05-13 at 2.28.08 PM](images/Screenshot%202024-05-13%20at%202.28.08%20PM.png)
Viewing the `GET` request, I was able to obtain the secret:
![Screenshot 2024-05-13 at 2.29.54 PM](images/Screenshot%202024-05-13%20at%202.29.54%20PM.png)

