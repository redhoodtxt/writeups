*This lab has an admin panel with a flawed multi-step process for changing a user's role. You can familiarize yourself with the admin panel by logging in using the credentials administrator:admin.
To solve the lab, log in using the credentials wiener:peter and exploit the flawed access controls to promote yourself to become an administrator.*

I logged in as administrator to try and see the process for changing a user's role. 
I tried to upgrade the user *carlos*, viewing the request in *Proxy*:
![[Screenshot 2024-05-13 at 4.25.29 PM.png]]
I sent this request to the *Repeater* first. 
I then logged into *wiener*'s credentials and obtained his session cookie after logging in:
![[Screenshot 2024-05-13 at 4.26.40 PM.png]]
I copied the session cookie and replaced the session cookie in the *Repeater* request with this, which solves the lab:
![[Screenshot 2024-05-13 at 4.27.34 PM.png]]
