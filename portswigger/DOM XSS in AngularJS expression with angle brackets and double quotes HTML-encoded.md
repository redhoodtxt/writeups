*This lab contains a DOM-based cross-site scripting vulnerability in a AngularJS expression within the search functionality.
AngularJS is a popular JavaScript library, which scans the contents of HTML nodes containing the ng-app attribute (also known as an AngularJS directive). When a directive is added to the HTML code, you can execute JavaScript expressions within double curly braces. This technique is useful when angle brackets are being encoded.
To solve this lab, perform a cross-site scripting attack that executes an AngularJS expression and calls the alert function.*

Greeted with a search box as shown:
![Screenshot 2024-05-14 at 2.12.25 PM](images/Screenshot%202024-05-14%20at%202.12.25%20PM.png)
I checked the HTML code using developer tools for the `ng-app` attribute, and sure enough, there was:
![Screenshot 2024-05-14 at 2.36.19 PM](images/Screenshot%202024-05-14%20at%202.36.19%20PM.png)
I then used the following payload I found from https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/XSS%20in%20Angular.md in the search box:
`{{constructor.constructor('alert(1)')()}}`

This solved the lab!
![Screenshot 2024-05-14 at 2.39.07 PM](images/Screenshot%202024-05-14%20at%202.39.07%20PM.png)
