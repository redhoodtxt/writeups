*This lab has a "Check stock" feature that parses XML input but does not display the result.
You can detect the blind XXE vulnerability by triggering out-of-band interactions with an external domain.
To solve the lab, use an external entity to make the XML parser issue a DNS lookup and HTTP request to Burp Collaborator.*

Checked the stock and viewed the request in *Proxy*:
![[Screenshot 2024-05-28 at 10.48.56 AM.png]]
Sent the request to *Repeater* and modified it to trigger a DNS lookup to *Collaborator*:
![[Screenshot 2024-05-28 at 10.52.26 AM.png]]
This caused the following lookup:
![[Screenshot 2024-05-28 at 10.53.30 AM.png]]
Solving the lab!