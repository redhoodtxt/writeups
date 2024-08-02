*This lab contains a blind OS command injection vulnerability in the feedback function.
The application executes a shell command containing the user-supplied details. The output from the command is not returned in the response. However, you can use output redirection to capture the output from the command. There is a writable folder at:
/var/www/images/
The application serves the images for the product catalog from this location. You can redirect the output from the injected command to a file in this folder, and then use the image loading URL to retrieve the contents of the file.
To solve the lab, execute the whoami command and retrieve the output.*

Submitted a feedback and sent the request to *Repeater* like before. I noticed that the images loaded had the query `image?filename=<image name>.jpg` appended to the URL. 

I had to try injecting a payload 
`|| whoami > /var/www/image/whoami.txt` (this will pipe `whoami` into the output file on the fileserver for images)
to each client input and checking the results using `<website>/image?filename=whoami.txt`. 
I had to make sure that the payload was  URL encoded as well, so that the payload is registered as a system command. 

After trying the payload at each point, I was not able to get any results. I modified the payload to the following: 
`|| whoami > /var/www/images/whoami.txt ||` adding `||` incase that there were additional commands run after a client input. I then encoded the payload and tried at each input: 
![Screenshot 2024-05-09 at 11.16.49 AM](images/Screenshot%202024-05-09%20at%2011.16.49%20AM.png)

The payload point was successful for the `email=` input, solving the lab when i accessed the `/image?filename=whoami.txt`.
