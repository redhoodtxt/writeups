*This lab contains a reflected cross-site scripting vulnerability in the search blog functionality. The reflection occurs inside a template string with angle brackets, single, and double quotes HTML encoded, and backticks escaped. To solve this lab, perform a cross-site scripting attack that calls the alert function inside the template string.*

- `<>,` ` '' `, and `""` HTML encoded
- ` ``escaped

Submitted a test search to view how it is processed:
![Screenshot 2024-05-16 at 5.23.14 PM](images/Screenshot%202024-05-16%20at%205.23.14%20PM.png)
Noticed that there was a backtick in the `message` variable, hence it was a template literal where I can embed expressions.
I then submitted the following payload:
`${alert(document.domain)}` into the search bar.

This gave the following successful result:
![Screenshot 2024-05-16 at 5.27.07 PM](images/Screenshot%202024-05-16%20at%205.27.07%20PM.png)
