*This lab is vulnerable to web cache poisoning because it handles input from an unkeyed header in an unsafe way. An unsuspecting user regularly visits the site's home page. To solve this lab, poison the cache with a response that executes alert(document.cookie) in the visitor's browser.*

Saw this request when clicking on a product:
![[Screenshot 2024-06-04 at 10.26.06 AM.png]]
Decided to *Guess Headers* with *Param Miner* and got the following results:
![[Screenshot 2024-06-04 at 10.29.40 AM.png]]
This tells me that `X-Forwarded-Host` is an unkeyed input. Let's take a look at the response:
![[Screenshot 2024-06-04 at 11.01.01 AM.png]]
We can take away a few things:
1. The cached response expires after a maximum of 30 seconds. 
2. `Age` indicates the age of the cache received, which means that this is the first request of its kind. This is also substantiated by `X-Cache` which indicates `miss` meaning the request we sent was the first of its kind and a relevant response is not found in the cache. 
3. most importantly, the `X-Forwarded-Host` header is used to generate a script dynamically that is `/resources/js/tracking.js`
I sent the request to the *Repeater* and modified the `X-Forwarded-Host` to include the exploit server. 
![[Screenshot 2024-06-04 at 10.36.14 AM.png]]
I then included the following script in my exploit server and stored the exploit:
`alert(document.cookie)`
I then modified the exploit URL to be `/resources/js/tracking.js` and stored the exploit:
![[Screenshot 2024-06-04 at 11.04.59 AM.png]]
I removed the cache buster (`/?umi4mqbmy=1`) from the request so that it will return the malicious response to the victims and sent the request:
![[Screenshot 2024-06-04 at 2.22.51 PM.png]]
This solves the lab:
![[Screenshot 2024-06-04 at 2.23.59 PM.png]]
