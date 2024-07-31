*This lab is vulnerable to routing-based SSRF via the Host header. You can exploit this to access an insecure intranet admin panel located on an internal IP address.
To solve the lab, access the internal admin panel located in the 192.168.0.0/24 range, then delete the user carlos.*

I accessed the the homepage.
I then sent this request to the Repeater and supplied the *Collaborator* domain to the `Host` header:
![[Screenshot 2024-06-06 at 4.59.24 PM.png]]
This performed a DNS lookup from the target application:
![[Screenshot 2024-06-06 at 5.00.45 PM.png]]
This indicates that the `Host` header is susceptible to routing SSRF attacks. 

I then replaced the `Host` header with that of the IP range and sent it to *Intruder*, where I added insertion points to the last digit of the IP. This is because it has a the subnet has a bitmask of /24, meaning only the last 8 bits(last digit) should be brute-forced to find the IP of the internal admin panel. 
I added the *Numbers* payload from 1-255 and unchecked the *Match host headers with target*:
![[Screenshot 2024-06-06 at 5.03.38 PM 1.png]]
![[Screenshot 2024-06-06 at 5.05.40 PM.png]]
Ran the attack to get the following results:
![[Screenshot 2024-06-06 at 5.09.17 PM.png]]
I then sent this request to *Repeater* and appended the `/admin` to the request line:
![[Screenshot 2024-06-06 at 5.11.46 PM.png]]
Opened the response in browser:
![[Screenshot 2024-06-06 at 5.13.01 PM.png]]
I then modified the request to change it according the requirements to delete(`POST` request, including `username` and `csrf` token parameters):
![[Screenshot 2024-06-06 at 5.14.48 PM.png]]
