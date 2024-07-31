*This lab makes flawed assumptions about the sequence of events in the login process. To solve the lab, exploit this flaw to bypass the lab's authentication, access the admin interface, and delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter*
- monitor login process
- look for bypass flaw - not brute-force 

Checked `/admin` to see the following: 
![[Screenshot 2024-05-10 at 2.21.40 PM.png]]
After viewing the login process through *Proxy*, I came across a request to select roles:
![[Screenshot 2024-05-10 at 2.49.01 PM.png]]
I decided to repeat the process so that I can capture the requests with *Intercept* and drop the `GET /role-selector` request and bypass authentication:
![[Screenshot 2024-05-10 at 2.50.23 PM.png]]
I then access `/` on the web browser after forwarding the remaining requests in *Intercept* to see a *Admin panel* at the `/` page:
![[Screenshot 2024-05-10 at 2.53.19 PM.png]]
Deleted *carlos* at the admin page!