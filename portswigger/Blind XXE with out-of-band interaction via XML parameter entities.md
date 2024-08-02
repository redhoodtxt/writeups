*This lab has a "Check stock" feature that parses XML input, but does not display any unexpected values, and blocks requests containing regular external entities.
To solve the lab, use a parameter entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.*

Checked stocked and viewed the request:
![Screenshot 2024-05-28 at 11.01.19 AM](images/Screenshot%202024-05-28%20at%2011.01.19%20AM.png)
Sent the request to *Repeater* and modified it to include parameter entities;
![Screenshot 2024-05-28 at 11.04.09 AM](images/Screenshot%202024-05-28%20at%2011.04.09%20AM.png)
This triggered the following DNS lookup to the *Collaborator*:
![Screenshot 2024-05-28 at 11.04.35 AM](images/Screenshot%202024-05-28%20at%2011.04.35%20AM.png)
