*This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality. The reflection occurs inside a JavaScript string with single quotes and backslashes escaped.
To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.*

Notices that the string was parsed into a script where it is assigned to the variable `searchTerms`:
![Screenshot 2024-05-16 at 1.12.29 PM](images/Screenshot%202024-05-16%20at%201.12.29%20PM.png)
I then used the following payload to try and break out of the script:
`</script><script><img src=1 onerror=alert("pwned")></script>`
From the following response, I deduced that I needed to break out of the quotes:
![Screenshot 2024-05-16 at 1.15.57 PM](images/Screenshot%202024-05-16%20at%201.15.57%20PM.png)
I modified the payload to as such:
`</script><img src=1 onerror=alert("pwned")>` : the additional script tags are not needed as with it the browser will read the whatever is within the additional `<script>` tag as javascript, so having the `img` tag inside the `script` tag will return and error or plaintext. 
This solves the lab!
![Screenshot 2024-05-16 at 2.25.27 PM](images/Screenshot%202024-05-16%20at%202.25.27%20PM.png)
