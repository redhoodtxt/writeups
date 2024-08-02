*This lab is vulnerable to routing-based SSRF due to its flawed parsing of the request's intended host. You can exploit this to access an insecure intranet admin panel located at an internal IP address.
To solve the lab, access the internal admin panel located in the 192.168.0.0/24 range, then delete the user carlos.*

Security measures placed when injecting an arbitrary value for the `Host` header:
![Screenshot 2024-06-06 at 5.41.13 PM](images/Screenshot%202024-06-06%20at%205.41.13%20PM.png)
I tried a variety of methods to elicit a lookup to the *Collaborator* server after this. The one that worked was supplying the absolute URL of the application while supplying the *Collaborator* domain in the `Host` header:

![Screenshot 2024-06-06 at 5.51.55 PM](images/Screenshot%202024-06-06%20at%205.51.55%20PM.png)
![Screenshot 2024-06-06 at 5.53.57 PM](images/Screenshot%202024-06-06%20at%205.53.57%20PM.png)
I then sent the request to the *Intruder* and 
1. selected the last digit as my payload insertion point
2. unchecked the *Update host header to match the target*
3. set the payload as *Numbers* with the range from 0-255
![Screenshot 2024-06-06 at 5.58.11 PM](images/Screenshot%202024-06-06%20at%205.58.11%20PM.png)
![Screenshot 2024-06-06 at 5.58.43 PM](images/Screenshot%202024-06-06%20at%205.58.43%20PM.png)
The results were as follows:
![Screenshot 2024-06-06 at 6.04.52 PM](images/Screenshot%202024-06-06%20at%206.04.52%20PM.png)
I sent the request to *Repeater* and appended `/admin` to the request line:
![Screenshot 2024-06-06 at 6.06.16 PM](images/Screenshot%202024-06-06%20at%206.06.16%20PM.png)
I then change the method to `POST`, added the `username` and `csrf` parameters and submitted the request to delete *carlos*:
![Screenshot 2024-06-06 at 6.08.53 PM](images/Screenshot%202024-06-06%20at%206.08.53%20PM.png)
