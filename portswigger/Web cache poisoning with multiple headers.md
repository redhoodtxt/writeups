*This lab contains a web cache poisoning vulnerability that is only exploitable when you use multiple headers to craft a malicious request. A user visits the home page roughly once a minute. To solve this lab, poison the cache with a response that executes alert(document.cookie) in the visitor's browser.*

Opened the home page and reloaded it to find the following request:
![[Screenshot 2024-06-04 at 3.42.51 PM.png]]
I used *Param Miner* to guess the headers that can be used:
![[Screenshot 2024-06-04 at 3.46.57 PM.png]]
![[Screenshot 2024-06-04 at 3.47.13 PM.png]]
Crafted the following in my exploit server:
![[Screenshot 2024-06-04 at 3.45.10 PM.png]]
Modified the request in *Repeater* to as such:
![[Screenshot 2024-06-04 at 3.49.58 PM.png]]
While the home page is a cache oracle, it will not execute the XSS as the file path for the `tracking.js` does not reflect the exploit server: 
![[Screenshot 2024-06-04 at 4.28.50 PM.png]]
I hence decided to target `/resources/js/tracking.js` request
I input the relevant payloads into the request and reloaded the home page a few times to solve the lab:
![[Screenshot 2024-06-04 at 4.30.55 PM.png]]
