*This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded. To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the alert function.*

Inserted the following payload into the search box to solve the lab:
`" autofocus onfocus=alert(document.domain) x="
![Screenshot 2024-05-16 at 9.57.57 AM](images/Screenshot%202024-05-16%20at%209.57.57%20AM.png)
