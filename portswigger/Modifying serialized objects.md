*This lab uses a serialization-based session mechanism and is vulnerable to privilege escalation as a result. To solve the lab, edit the serialized object in the session cookie to exploit this vulnerability and gain administrative privileges. Then, delete the user carlos.
You can log in to your own account using the following credentials: wiener:peter*

Noticed the following issue after logging in:
![Screenshot 2024-05-30 at 10.53.24 AM](images/Screenshot%202024-05-30%20at%2010.53.24%20AM.png)
Decoding the cookie using *Inspector* gives the following:
![Screenshot 2024-05-30 at 10.56.06 AM](images/Screenshot%202024-05-30%20at%2010.56.06%20AM.png)
It seems that there is a Boolean attribute that checks if a user is an admin or not.
I sent the request to the *Repeater* and changed the value of the `admin` to 1:
There was an error when i sent the request, likely a padding issue:
![Screenshot 2024-05-30 at 11.07.05 AM](images/Screenshot%202024-05-30%20at%2011.07.05%20AM.png)
Removed the padding (`=%3d`) and resent the request, which gave me admin access:
![Screenshot 2024-05-30 at 11.08.28 AM](images/Screenshot%202024-05-30%20at%2011.08.28%20AM.png)
Navigated to the `/admin` page:
![Screenshot 2024-05-30 at 11.09.44 AM](images/Screenshot%202024-05-30%20at%2011.09.44%20AM.png)
Navigated to the URL to delete *carlos*:
![Screenshot 2024-05-30 at 11.11.06 AM](images/Screenshot%202024-05-30%20at%2011.11.06%20AM.png)
