*This lab is vulnerable to routing-based SSRF via the Host header. Although the front-end server may initially appear to perform robust validation of the Host header, it makes assumptions about all requests on a connection based on the first request it receives.
To solve the lab, exploit this behavior to access an internal admin panel located at 192.168.0.1/admin, then delete the user carlos.*

Sent the homepage request *Repeater* and duplicated the request (DO NOT SEND TO REPEATER AGAIN)

I then changed the `Connection` header to `keep-alive` for both requests:

I added both the requests to the same group (right click on any tab):
![Screenshot 2024-06-06 at 6.45.32 PM](images/Screenshot%202024-06-06%20at%206.45.32%20PM.png)

Then I selected *Send group (single connection)* from the drop down button beside *Send*:
![Screenshot 2024-06-06 at 6.46.36 PM](images/Screenshot%202024-06-06%20at%206.46.36%20PM.png)
I then modified the duplicate request to contain the target IP in the `Host` header, with `/admin` appended to its request line:
![Screenshot 2024-06-06 at 7.09.34 PM](images/Screenshot%202024-06-06%20at%207.09.34%20PM.png)
Then i sent the request:
![Screenshot 2024-06-06 at 7.11.48 PM](images/Screenshot%202024-06-06%20at%207.11.48%20PM.png)
Modified the request line to `POST /admin/delete HTTP/1.1` while including the `username` and `csrf` parameters:
![Screenshot 2024-06-06 at 7.16.49 PM](images/Screenshot%202024-06-06%20at%207.16.49%20PM.png)
