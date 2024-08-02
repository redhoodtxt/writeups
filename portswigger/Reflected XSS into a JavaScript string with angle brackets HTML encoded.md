*This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets are encoded. The reflection occurs inside a JavaScript string. To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.*

Injected the following payload to solve the lab:
`;alert(document.domain)//`
![Screenshot 2024-05-16 at 3.12.14 PM](images/Screenshot%202024-05-16%20at%203.12.14%20PM.png)