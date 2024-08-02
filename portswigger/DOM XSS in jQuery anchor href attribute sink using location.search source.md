*This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's $ selector function to find an anchor element, and changes its href attribute using data from location.search.
To solve this lab, make the "back" link alert document.cookie*

Accessed the *Submit feedback* page and submitted a test feedback:
![Screenshot 2024-05-14 at 12.51.25 PM](images/Screenshot%202024-05-14%20at%2012.51.25%20PM.png)

Opened the developer console and searched for the script tag, finding the following:
![Screenshot 2024-05-14 at 12.53.12 PM](images/Screenshot%202024-05-14%20at%2012.53.12%20PM.png)
this function: 
1. searches for an element with `backlink` as its id
2. changes that element's attribute to `href`, where the value is retrieved(.get) from the params object created using `windows.location.search`. it then retrieves the value of the query parameter of `returnPath`, which is `/`
I then decided to try and manipulate the value of the `returnPath` query parameter to as such
`?returnPath=javascript:alert(document.cookie)`

Pressing the back button will result in the following, solving the lab:
![Screenshot 2024-05-14 at 12.59.20 PM](images/Screenshot%202024-05-14%20at%2012.59.20%20PM.png)
