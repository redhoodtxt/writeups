*This lab makes an assumption about the privilege level of the user based on the HTTP Host header.
To solve the lab, access the admin panel and delete the user carlos.*

Checked `robots.txt` to see if the directory name for the admin panel is there:
![Screenshot 2024-06-05 at 6.30.46 PM](images/Screenshot%202024-06-05%20at%206.30.46%20PM.png)
We see that the admin panel is at `/admin`. Let's navigate to this directory and see if we can access it first:
![Screenshot 2024-06-05 at 6.31.58 PM](images/Screenshot%202024-06-05%20at%206.31.58%20PM.png)
We see that the admin panel is only available to local users, indicating that the `Host` header may have to be from `localhost`.
Let's test the `Host` header to see if it is subject to host header injection. 
I replaced the value of the `Host` header to that of an arbitrary domain `example.com` and checked the response:
![Screenshot 2024-06-05 at 6.35.37 PM](images/Screenshot%202024-06-05%20at%206.35.37%20PM.png)
As you can see, the application still loads with a different `Host` header value. Let's change the request line to `/admin` and do the same thing:
![Screenshot 2024-06-05 at 6.37.04 PM](images/Screenshot%202024-06-05%20at%206.37.04%20PM.png)
The same error pops up. Let's change the value of the `Host` header to `localhost`:
![Screenshot 2024-06-05 at 6.38.13 PM](images/Screenshot%202024-06-05%20at%206.38.13%20PM.png)
We were able to successfully log in to the admin panel. Let's navigate to the relevant directory to delete *carlos*:
![Screenshot 2024-06-05 at 6.41.05 PM](images/Screenshot%202024-06-05%20at%206.41.05%20PM.png)
