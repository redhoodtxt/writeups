=thi*This lab contains a reflected XSS vulnerability in the search functionality but uses a web application firewall (WAF) to protect against common XSS vectors.
To solve the lab, perform a cross-site scripting attack that bypasses the WAF and calls the print() function.*

Greeted with a search box:
![Screenshot 2024-05-15 at 9.31.26 AM](images/Screenshot%202024-05-15%20at%209.31.26%20AM.png)
While attempting to parse XSS payloads into the search box, I found that most tags (`<script>`,`<img>`,`<iframe>`) were not allowed:
![Screenshot 2024-05-15 at 9.38.50 AM](images/Screenshot%202024-05-15%20at%209.38.50%20AM.png)
However, when I used the `<body>` tag with the `<onload>` attribute, only the `onload` attribute is not allowed:
![Screenshot 2024-05-15 at 9.42.42 AM](images/Screenshot%202024-05-15%20at%209.42.42%20AM.png)
I hence decided to brute-force to find right attribute that can trigger XSS.
I sent the request to *Intruder*, and added the following payload:
`<body onload = 1>`
- i used `1` as the value as it does not cause an error, where the event will just perform a no-op (no operation)
I then set the payload markers on the event:
![Screenshot 2024-05-15 at 12.49.00 PM](images/Screenshot%202024-05-15%20at%2012.49.00%20PM.png)
I then copied the events from the XSS cheatsheet and pasted into the payload settings:
![Screenshot 2024-05-15 at 12.49.56 PM](images/Screenshot%202024-05-15%20at%2012.49.56%20PM.png)
This gave the following results:
![Screenshot 2024-05-15 at 12.53.54 PM](images/Screenshot%202024-05-15%20at%2012.53.54%20PM.png)
I then copied this query parameter and its value and pasted it in my exploit server, in the format as follows:
```
<iframe src="https:<url>/?search=<body onresize=print()>" onload=this.style.width='100px'>
```
![Screenshot 2024-05-15 at 12.59.35 PM](images/Screenshot%202024-05-15%20at%2012.59.35%20PM.png)
This resizes the window on load. Upon resizing, it executes `print()`.
