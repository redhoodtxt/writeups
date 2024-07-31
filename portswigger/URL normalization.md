*This lab contains an XSS vulnerability that is not directly exploitable due to browser URL-encoding.
To solve the lab, take advantage of the cache's normalization process to exploit this vulnerability. Find the XSS vulnerability and inject a payload that will execute alert(1) in the victim's browser. Then, deliver the malicious URL to the victim.*

Loaded the homepage and sent the request to the *Repeater*. So I tried to generate an error message to get a verbose output. I got the following after placing an arbitrary directory:
![[Screenshot 2024-06-05 at 5.46.46 PM.png]]
We can see that the directory is reflected in the homepage, so we can test for reflected XSS. I tried the following payload while adding cache busters to unkeyed inputs:
`/lol</p><script>alert(1)</script> `
This caused a reflected XSS:
![[Screenshot 2024-06-05 at 5.49.44 PM.png]]
I removed the cache busters and sent the request again to poison the cache, then sent the malicious URL to the victim immediately:
![[Screenshot 2024-06-05 at 5.54.25 PM.png]]
![[Screenshot 2024-06-05 at 5.54.51 PM.png]]
Refreshed the homepage to solve the lab:
![[Screenshot 2024-06-05 at 5.55.55 PM.png]]
