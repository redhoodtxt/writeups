*This lab is vulnerable to web cache poisoning because the query string is unkeyed. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the home page with a response that executes alert(1) in the victim's browser.*

I reloaded the page and sent the homepage request to *Repeater* adding a cache buster to the request line. From the below image, since there was a hit, we can deduce that the query string is a unkeyed:
![[Screenshot 2024-06-05 at 10.42.31 AM.png]]
I did some trial and error of finding under which header I can insert the cache buster by:
1. sending the original request after 35s in *Repeater*
2. creating a copy of the original request in *Repeater*
3. modifying the copy to add a cache buster to each of the headers one at a time and sending the modified request
4. checking to see if there is a `hit` or `miss` after sending the modified request within 35s of sending the original request
	- if there is a `miss` this means that the cache worked.
I noticed that when there is a cache `miss` with the modified request, it is reflected in the response in the following:
![[Screenshot 2024-06-05 at 11.02.35 AM.png]]
It doesn't register as a script, which explains why I don't get a alert notification when I show the response in the browser. 
I need to find a way to break out of the string to reflect my XSS. 
I modified my payload to be as such:
`GET /?xss='/><script>alert(1)</script>`
This caused the XSS to be reflected:
![[Screenshot 2024-06-05 at 11.05.40 AM.png]]
I then removed the cache busters, changed the user agent to that of a device using Chrome(important since the victim is using Chrome) and repeated the request again to solve the lab:
![[Screenshot 2024-06-05 at 1.36.23 PM.png]]
