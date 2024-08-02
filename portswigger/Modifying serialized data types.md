*This lab uses a serialization-based session mechanism and is vulnerable to authentication bypass as a result. To solve the lab, edit the serialized object in the session cookie to access the administrator account. Then, delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter*

Came across the following after logging in:
![Screenshot 2024-05-30 at 1.20.22 PM](images/Screenshot%202024-05-30%20at%201.20.22%20PM.png)
Sent the request to the *Repeater* and modified the cookie as such:
![Screenshot 2024-05-30 at 1.21.37 PM](images/Screenshot%202024-05-30%20at%201.21.37%20PM.png)
the changes were:
1. modified the `GET` request to have the `id` of *administrator*
2. changed the username in the cookie to `administrator` and the corresponding length of the string to `13`
3. changed the data type of the access token to `i` (integer) and its corresponding value to 0
4. made the padding 0 for this specific request
I then navigated to the corresponding URL to delete carlos:
![Screenshot 2024-05-30 at 1.25.36 PM](images/Screenshot%202024-05-30%20at%201.25.36%20PM.png)
