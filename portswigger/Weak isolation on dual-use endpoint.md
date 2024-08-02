*This lab makes a flawed assumption about the user's privilege level based on their input. As a result, you can exploit the logic of its account management features to gain access to arbitrary users' accounts. To solve the lab, access the administrator account and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter*

After logging in with the given credentials, I tried to manipulate the username and change the password for *administrator*:

![Screenshot 2024-05-10 at 12.13.50 PM](images/Screenshot%202024-05-10%20at%2012.13.50%20PM.png)
I sent the request to *Repeater* and removed the `current-password` parameter, sending the request afterwards:
![Screenshot 2024-05-10 at 1.34.52 PM](images/Screenshot%202024-05-10%20at%201.34.52%20PM.png)
Then logged into the administrator account with the new credentials and had the *admin panel* available:
![Screenshot 2024-05-10 at 1.35.56 PM](images/Screenshot%202024-05-10%20at%201.35.56%20PM.png)

Deleted *carlos* to solve the lab!