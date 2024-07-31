*This lab has an unprotected admin panel. Solve the lab by deleting the user carlos.*

Greeted with the same page as before, moved to the login page as shown : 
![[unprotected admin functionality.png]]

Decided to check `robots.txt` directory to see if there was any useful information : 
```HTML
User-agent: *
Disallow: /administrator-panel
```
Traversed to `/administrator-panel`. 
![[Screenshot 2024-04-29 at 5.27.24 PM.png]]
Deleted *carlos*. 

Done!