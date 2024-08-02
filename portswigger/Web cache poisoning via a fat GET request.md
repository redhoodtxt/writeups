*This lab is vulnerable to web cache poisoning. It accepts GET requests that have a body, but does not include the body in the cache key. A user regularly visits this site's home page using Chrome.
To solve the lab, poison the cache with a response that executes alert(1) in the victim's browser.*

After the request for the homepage loaded, there was the same request for `/js/geolocate.js?callback=setCountryCookie`
![Screenshot 2024-06-05 at 4.17.15 PM](images/Screenshot%202024-06-05%20at%204.17.15%20PM.png)
I sent the request to the *Repeater* and inserted the following payload as a body:
`callback=alert(1)`
This resulted in the alert firing, solving the lab:
![Screenshot 2024-06-05 at 4.15.51 PM](images/Screenshot%202024-06-05%20at%204.15.51%20PM.png)
