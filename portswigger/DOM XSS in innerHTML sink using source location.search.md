*This lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an innerHTML assignment, which changes the HTML contents of a div element, using data from location.search.
To solve this lab, perform a cross-site scripting attack that calls the alert function.*

Greeted with a search box as shown:
![Screenshot 2024-05-14 at 11.16.43 AM](images/Screenshot%202024-05-14%20at%2011.16.43%20AM.png)
I opened my developer console, typed in "test" into the search box and observed the response:
![Screenshot 2024-05-14 at 11.19.14 AM](images/Screenshot%202024-05-14%20at%2011.19.14%20AM.png)
1. there is a `search` query parameter in the URL
2. the string parsed into the `search` parameter is assigned and id `searchMessage`
I then searched for script tags where the id `searchMessage` pops up:
![Screenshot 2024-05-14 at 11.21.48 AM](images/Screenshot%202024-05-14%20at%2011.21.48%20AM.png)
This script:
1. process the query parameter value, and retrieves the value of the `search` parameter, where it is assigned to the `query` variable
2. if `query` is not null, it executes the function
	- the function gets the element with the id `searchMessage` and uses `innerHTML` to write the contents of the element with the contents of the variable `query`
As `.innerHTML` does not allow script tags to be used, I can parse in the following payload into the URL to check for XSS:
`<img src = 1 onerror=alert(1)>`
This results in the following, which solves the lab:
![Screenshot 2024-05-14 at 11.28.20 AM](images/Screenshot%202024-05-14%20at%2011.28.20%20AM.png)
