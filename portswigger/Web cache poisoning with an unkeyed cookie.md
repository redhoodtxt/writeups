*This lab is vulnerable to web cache poisoning because cookies aren't included in the cache key. An unsuspecting user regularly visits the site's home page. To solve this lab, poison the cache with a response that executes alert(1) in the visitor's browser.*

After reloading the homepage, I was given a request with a cookie, with a few interesting things:
![Screenshot 2024-06-04 at 2.32.16 PM](images/Screenshot%202024-06-04%20at%202.32.16%20PM.png)
I can possibly manipulate the value of `fehost` to include the script for XSS.
I inserted the following payload after sending the request to *Repeater*:
`"}</script><script>alert(1)</script><script>`
![Screenshot 2024-06-04 at 3.00.42 PM](images/Screenshot%202024-06-04%20at%203.00.42%20PM.png)
![Screenshot 2024-06-04 at 3.01.38 PM](images/Screenshot%202024-06-04%20at%203.01.38%20PM.png)
