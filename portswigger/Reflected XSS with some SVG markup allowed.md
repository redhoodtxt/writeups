*This lab has a simple reflected XSS vulnerability. The site is blocking common tags but misses some SVG tags and events.
To solve the lab, perform a cross-site scripting attack that calls the alert() function.*

Tried to insert the following `svg` XSS payload:
`<svg/onload=alert('XSS')>`
This gave me the following error:
![[Screenshot 2024-05-15 at 3.07.12 PM.png]]
I then sent the request to *Intruder*. I set the payload markers on the event and pasted the events payload list in the payload settings. I then ran the attack to receive the following results:
![[Screenshot 2024-05-15 at 3.09.07 PM.png]]
This tells me that the `onbegin` payload was successful. `onbegin` events fire immediately when the element's timeline begins. I replaced the `onload` to `onbegin`, but this did not reflect any alerts. 

Knowing that the `svg` element and `onbegin` attribute works, I tried different payloads that were `svg` markups, which contains  these two. I eventually found that the following payload:
`<svg><animatetransform onbegin=alert(1) attributeName=transform>` gave me the alert, solving the lab!
![[Screenshot 2024-05-16 at 9.42.13 AM.png]]
