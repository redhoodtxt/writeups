*This lab is vulnerable to web cache poisoning due to discrepancies in how the cache and the back-end application handle ambiguous requests. An unsuspecting user regularly visits the site's home page.
To solve the lab, poison the cache so the home page executes alert(document.cookie) in the victim's browser.*

I noticed that there was a file called `tracking.js` generated when accessing the homepage:
![Screenshot 2024-06-06 at 12.15.27 PM](images/Screenshot%202024-06-06%20at%2012.15.27%20PM.png)
We can potentially overwrite the file to instead load our exploit which contains our XSS payload. I hence crafted my exploit to be the following:
![Screenshot 2024-06-06 at 12.18.06 PM](images/Screenshot%202024-06-06%20at%2012.18.06%20PM.png)
We now need a way to deliver our exploit to the victim when they access the homepage. As mentioned by the lab description, we can try to deliver it through a poisoned cached response where we modify the `Host` header to point to our domain. 
In this case, I'll use the `/` as our cache oracle where we perform the request, since we want the XSS to pop up on the victim's homepage.

I sent the `/` request to *Repeater* and then changed the `Host` header to an arbitrary value to see if it is prone to `Host` header injection this way:
![Screenshot 2024-06-06 at 1.01.47 PM](images/Screenshot%202024-06-06%20at%201.01.47%20PM.png)
There seems to be a error when changing the `Host` to an arbitrary value, so let's try to cause some discrepancies with ambiguous requests. 

After sending the original request, I first tried to use duplicate `Host` headers in a copy of the original request, swapping the domains between the 2 instances. I also added cache busters to the modified request to make sure that the victim does not receive the malicious response yet. i also added a cache buster to the request:
![Screenshot 2024-06-06 at 1.16.48 PM](images/Screenshot%202024-06-06%20at%201.16.48%20PM.png)
I then removed the cache buster and resent the request, poisoning the cache and reloading the homepage to solve the lab:
![Screenshot 2024-06-06 at 1.19.27 PM](images/Screenshot%202024-06-06%20at%201.19.27%20PM.png)
