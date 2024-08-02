*This lab's administration interface has an authentication bypass vulnerability, but it is impractical to exploit without knowledge of a custom HTTP header used by the front-end.
To solve the lab, obtain the header name then use it to bypass the lab's authentication. Access the admin interface and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter*

From the description, the goal is bypass into the admin interface. I tried to access the admin page first, checking `/admin`:
![Screenshot 2024-05-08 at 1.39.12 PM](images/Screenshot%202024-05-08%20at%201.39.12%20PM.png)
This verifies that we do not need to brute-force the admin's credentials to enter the admin interface. 
I tried enumerating the hidden custom header using `HTTP TRACE` method in the repeater, using `POST/login` request:
`HTTP POST` -> `HTTP TRACE`
![Screenshot 2024-05-08 at 1.42.16 PM](images/Screenshot%202024-05-08%20at%201.42.16%20PM.png)
I appended the custom header into the `/admin` request, ensuring that the header was before the `csrf` token so that it is processed correctly and changed the IP in the custom header to my own local IP:
![Screenshot 2024-05-08 at 1.47.19 PM](images/Screenshot%202024-05-08%20at%201.47.19%20PM.png)
After getting the page to render, clicking delete will not work as you will be redirected to the same error message at `/admin` as before. I sent the delete request to repeater and added in the customer header with my IP: 
![Screenshot 2024-05-08 at 1.49.58 PM](images/Screenshot%202024-05-08%20at%201.49.58%20PM.png)

