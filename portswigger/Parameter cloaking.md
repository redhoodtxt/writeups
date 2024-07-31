*This lab is vulnerable to web cache poisoning because it excludes a certain parameter from the cache key. There is also inconsistent parameter parsing between the cache and the back-end. A user regularly visits this site's home page using Chrome.
To solve the lab, use the parameter cloaking technique to poison the cache with a response that executes alert(1) in the victim's browser.*

Noticed the following parameter in the response after loading the homepage:
![[Screenshot 2024-06-05 at 3.12.02 PM.png]]
I looked for `/js/geolocate.js` in the *Proxy*:
![[Screenshot 2024-06-05 at 3.29.06 PM.png]]
We see that the `setCountryCookie` function is executed with the `callback` function.
The hint mentioned that a certain UTM analytics parameter is excluded, so I tried to insert the `utm_content` parameter into the above request after sending it to *Repeater*. I sent the original request to create a cached response and then sent the modified request to see if I get a `hit` (meaning the cached response is returned).
1. sent the original request first to generate the cached response:
	![[Screenshot 2024-06-05 at 3.33.56 PM.png]]
2. then sent the modified request after sending the original request:
	![[Screenshot 2024-06-05 at 3.35.16 PM.png]]
This confirms that the `utm_content` query parameter is indeed not included in the cache key, so we use it to hide another `callback` query parameter containing our payload in the request line, so that the server processes our payload instead of the original `setCountryCookie` function.
I generated the following payload:
`GET /js/geolocate.js?callback=setCountryCookie&utm_content=lol;callback=alert(1)`
I sent this request, causing the XSS to execute, solving the lab:
![[Screenshot 2024-06-05 at 3.40.50 PM.png]]
