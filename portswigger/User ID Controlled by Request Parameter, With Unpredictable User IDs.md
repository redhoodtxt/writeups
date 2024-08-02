*This lab has a horizontal privilege escalation vulnerability on the user account page, but identifies users with GUIDs.
To solve the lab, find the GUID for carlos, then submit his API key as the solution.
You can log in to your own account using the following credentials: wiener:peter*

Greeted with the following page consisting of blog posts. 
![user id controlled by request param with unpredictable user id](images/user%20id%20controlled%20by%20request%20param%20with%20unpredictable%20user%20id.png)

The goal is to find the GUID of *carlos*, so I skimmed through through the posts to find a post by *carlos*.
Ended up finding the following by *carlos* with his name as a hyperlink.

![Screenshot 2024-04-30 at 9.06.24 AM](images/Screenshot%202024-04-30%20at%209.06.24%20AM.png)

I then clicked on the *carlos* hyperlink, which gave me the GUID of carlos. I took note of the GUID given : 

`?id=36d5bb20-fad9-4764-b118-1646289553f0`

Next, I tried logging into my own account. I was given my own API key upon logging in : 

![Screenshot 2024-04-30 at 9.29.05 AM](images/Screenshot%202024-04-30%20at%209.29.05%20AM.png)

I then changed the GUID in the URL to that of *carlos*. 

![Screenshot 2024-04-30 at 9.30.04 AM](images/Screenshot%202024-04-30%20at%209.30.04%20AM.png)

Was given the API of *carlos* : 

![Screenshot 2024-04-30 at 9.30.56 AM](images/Screenshot%202024-04-30%20at%209.30.56%20AM.png)

Submitted the API key!