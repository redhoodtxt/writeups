*This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.
To solve the lab, perform a cross-site scripting attack that calls the alert function.*

Greeted with the following page, where there is a input field for searching the blog as shown:
![[Screenshot 2024-05-13 at 6.01.40 PM.png]]
I input the following javascript into the search box:
`<script>alert("XSS")</script>` - this will create a pop-up with the string "XSS". 
![[Screenshot 2024-05-13 at 6.03.54 PM.png]]
This gave the following pop-up, solving the lab:
![[Screenshot 2024-05-13 at 6.04.16 PM.png]]
