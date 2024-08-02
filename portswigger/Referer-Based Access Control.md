*This lab controls access to certain admin functionality based on the Referer header. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.
To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator.*

Familiarised myself with the admin functionality by logging in as admin, upgrading *carlos*, all while viewing the requests in *Proxy*. 
Noticed that there was a `Referer` header in the request of `/admin-roles?username=carlos&action=upgrade`, with the `Referer` being the admin page. 
![Screenshot 2024-05-13 at 4.37.44 PM](images/Screenshot%202024-05-13%20at%204.37.44%20PM.png)
I can try forge a request to upgrade my own account *wiener* by using the same `Referer`!
I sent the above request to *Repeater* first. 
I then logged in with *wiener* using the given credentials and copied the session cookie for my account:
![Screenshot 2024-05-13 at 4.42.48 PM](images/Screenshot%202024-05-13%20at%204.42.48%20PM.png)
I then replaced the session cookie in the *Repeater* with the above cookie and changed the `username` parameter value to `wiener`. 
This solves the lab!
![Screenshot 2024-05-13 at 4.45.11 PM](images/Screenshot%202024-05-13%20at%204.45.11%20PM.png)