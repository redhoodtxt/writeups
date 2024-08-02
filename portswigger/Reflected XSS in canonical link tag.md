*This lab reflects user input in a canonical link tag and escapes angle brackets.
To solve the lab, perform a cross-site scripting attack on the home page that injects an attribute that calls the alert function.
To assist with your exploit, you can assume that the simulated user will press the following key combinations:
```
ALT+SHIFT+X
CTRL+ALT+X
Alt+X
```
Please note that the intended solution to this lab is only possible in Chrome.*

Noticed that there was a canonical link tag upon loading the page:
![Screenshot 2024-05-16 at 10.57.06 AM 1](images/Screenshot%202024-05-16%20at%2010.57.06%20AM%201.png)
I input the following payload in the root URL:
`?'accesskey='x'onclick='alert(1)`

This will add the `x` shortcut to load the page, and when triggered, will fire the `onclick` event to create the alert.
