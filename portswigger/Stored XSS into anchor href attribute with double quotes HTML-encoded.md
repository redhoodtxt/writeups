*This lab contains a stored cross-site scripting vulnerability in the comment functionality. To solve this lab, submit a comment that calls the alert function when the comment author name is clicked.*

Filled out the comment functionality for a comment, noticing the following once it had been posted:
![[Screenshot 2024-05-16 at 10.34.58 AM.png]]
After filling up the *website* field, the name is coloured in purple and has a link embedded.
I decided to post another comment, inserting `javascript:alert(1)` into the *website* field. This solves the lab!
![[Screenshot 2024-05-16 at 10.37.04 AM.png]]
