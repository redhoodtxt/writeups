*This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response.
To solve the lab, exploit the blind OS command injection vulnerability to cause a 10 second delay.*

Clicked on the *Submit feedback* button and submitted a feedback response:
![Screenshot 2024-05-08 at 5.37.17 PM](images/Screenshot%202024-05-08%20at%205.37.17%20PM.png)
Sent it to *Intruder*, defined the payload point to be the message value, and then scanned the defined insertion points. This produced a time delay with the following payload, completing the lab.
![Screenshot 2024-05-08 at 5.39.16 PM](images/Screenshot%202024-05-08%20at%205.39.16%20PM.png)


Clicking on the *Submit feedback* form, I filled up the feedback and submitted it, sending the request captured by *Proxy* to the *Repeater*. 
![Screenshot 2024-05-09 at 10.44.43 AM](images/Screenshot%202024-05-09%20at%2010.44.43%20AM.png)
I had to test individually for each client input to see which input is parsed into a system command in the back end. I deduced that the input for email is parsed in the backend, eg. `mail $(email)`. 
I decided to inject the following payload:
`|| ping -c 10 127.0.0.1 &` where i would leave the input for `email=` blank. This would throw an error on the system command for email, leading my injected command to be executed. I added the `&` at the end of my payload to let the process run in the background. 
I had to ensure that the whole payload was url-encoded so that the following client inputs will not be affected, keeping the colour of the client inputs the same in Burp:
![Screenshot 2024-05-09 at 10.49.51 AM](images/Screenshot%202024-05-09%20at%2010.49.51%20AM.png)
This successfully made the application sleep for 10s!
