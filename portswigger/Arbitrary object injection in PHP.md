*This lab uses a serialization-based session mechanism and is vulnerable to arbitrary object injection as a result. To solve the lab, create and inject a malicious serialized object to delete the morale.txt file from Carlos's home directory. You will need to obtain source code access to solve this lab.
You can log in to your own account using the following credentials: wiener:peter*
Came across the following comment:
![Screenshot 2024-05-30 at 3.43.47 PM](images/Screenshot%202024-05-30%20at%203.43.47%20PM.png)
The file path came up to an empty page. I checked the hints, which said that appending `~` to a filename allows us to access source code by retrieving an editor-generated backup file. I did as such, to receive the following:
![Screenshot 2024-05-30 at 3.51.23 PM](images/Screenshot%202024-05-30%20at%203.51.23%20PM.png)
I modified the cookie to the following, which will automatically invoke the `__destruct` function:
![Screenshot 2024-05-30 at 4.32.25 PM 1](images/Screenshot%202024-05-30%20at%204.32.25%20PM%201.png)
This solves the lab. 