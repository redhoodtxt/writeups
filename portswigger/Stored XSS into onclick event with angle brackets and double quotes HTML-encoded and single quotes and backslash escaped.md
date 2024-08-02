*This lab contains a stored cross-site scripting vulnerability in the comment functionality.
To solve this lab, submit a comment that calls the alert function when the comment author name is clicked.*

Submitted a test comment and noticed that there was a `href` attribute for the `a` tag where the name is:
![Screenshot 2024-05-16 at 4.34.10 PM](images/Screenshot%202024-05-16%20at%204.34.10%20PM.png)
There was also a `onclick` event where it sends the user to the website upon clicking the name. I can potentially exploit this by injecting my own payload into the `onclick` event. As the `<>` and `"` are HTML encoded, with the single quotes and `\` escaped, I can try to HTML encode my payload to parse through the server side and be decoded by the browser to execute it. 
I used the following payload: 
`&apos;-alert(document.domain)-&apos;` in the website field as the suffix to the website:
![Screenshot 2024-05-16 at 4.46.10 PM](images/Screenshot%202024-05-16%20at%204.46.10%20PM.png)
This gave the following successful result:
![Screenshot 2024-05-16 at 4.47.46 PM](images/Screenshot%202024-05-16%20at%204.47.46%20PM.png)