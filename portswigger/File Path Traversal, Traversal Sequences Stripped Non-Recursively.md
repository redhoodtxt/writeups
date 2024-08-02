*This lab contains a path traversal vulnerability in the display of product images.
The application strips path traversal sequences from the user-supplied filename before using it.
To solve the lab, retrieve the contents of the /etc/passwd file.*

Clicked on a product and then opened its image, then inputting the following into the `filename` parameter:
`....//....//....//`
This output the contents of /etc/shadow:
![Screenshot 2024-05-07 at 5.14.42 PM](images/Screenshot%202024-05-07%20at%205.14.42%20PM.png)
