*This lab contains a DOM-based cross-site scripting vulnerability on the home page. It uses jQuery's $() selector function to auto-scroll to a given post, whose title is passed via the location.hash property.
To solve the lab, deliver an exploit to the victim that calls the print() function in their browser.*

Accessed the page, opened my developer console and searched for script tags, coming across the following:
![Screenshot 2024-05-14 at 1.41.42 PM](images/Screenshot%202024-05-14%20at%201.41.42%20PM.png)
- this function:
	1. scrolls the window to the relevant blog when the hash contains part or all of the string in the URL
I decided to test this by inputting the hash `#Spider` into the URL, and the following blog scrolled to view as expected:
![Screenshot 2024-05-14 at 1.46.09 PM](images/Screenshot%202024-05-14%20at%201.46.09%20PM.png)
I went into my exploit server and input the following into the body :
`<iframe src="https://0a0300f003941747800fdae200830004.web-security-academy.net/#" onload="this.src+='<img src=1 onerror=print()>'">`
This is how it looked like:
![Screenshot 2024-05-14 at 2.03.47 PM](images/Screenshot%202024-05-14%20at%202.03.47%20PM.png)
This sends a phishing link to the victim, who upon clicking it, will be redirected to the vulnerable website where the print function will open up. 
I delivered the exploit to the victim, which solved the lab!
