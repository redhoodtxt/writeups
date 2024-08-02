*This lab contains a stored cross-site scripting vulnerability in the comment functionality.
To solve this lab, submit a comment that calls the alert function when the blog post is viewed.*

Greeted with the following page with blog posts:
![Screenshot 2024-05-13 at 6.44.33 PM](images/Screenshot%202024-05-13%20at%206.44.33%20PM.png)
Clicked on the first blog post to see there was a comment functionality:
![Screenshot 2024-05-13 at 6.46.07 PM](images/Screenshot%202024-05-13%20at%206.46.07%20PM.png)
I decided to see if the comment section could be subjected to stored XSS. I wrote the following payload in it:
`<script>alert("XSS")</script>` 
I then posted the comment. 
If we went back to the blog post after commenting the malicious script, the following pop-up appears:
![Screenshot 2024-05-13 at 6.48.35 PM](images/Screenshot%202024-05-13%20at%206.48.35%20PM.png)
Done!