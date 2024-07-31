*This lab makes flawed assumptions about the sequence of events in the purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter*

Logged in and tried buying a cheaper item, viewing the purchasing workflow using *Proxy*:
![[Screenshot 2024-05-10 at 2.09.48 PM.png]]

I changed the `productId` parameter value to 1 (that of the jacket) and changed the `redir` parameter value to `CART` in *Repeater* and sent the request, which solved the lab:
![[Screenshot 2024-05-10 at 2.11.45 PM.png]]
