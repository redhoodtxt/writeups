*This lab is vulnerable to web cache poisoning because it excludes a certain parameter from the cache key. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the cache with a response that executes alert(1) in the victim's browser.*

Sent the homepage request to *Repeater*. Issued the request to get it in the cache. I then added in a arbitrary query string to see if I am returned a cached response from the original request (`hit`).
After doing so, I found that I am returned a cached response despite changing the request line:
![[Screenshot 2024-06-05 at 1.59.14 PM 1.png]]
This means that query strings are excluded from the cache key. However as mentioned in the hint, some websites exclude UTM analytics parameters from the cache key. 
We can hence use that as a possible injection point for payload. 
I injected the following payload to solve the lab:
`GET /?utm_content='/><script>alert(1)</script>`
![[Screenshot 2024-06-05 at 1.55.02 PM.png]]