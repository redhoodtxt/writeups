*This lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search, which you can control using the website URL.
To solve this lab, perform a cross-site scripting attack that calls the alert function.*

Loaded into the page as shown, where there was a search box:
![Screenshot 2024-05-14 at 9.34.25 AM](images/Screenshot%202024-05-14%20at%209.34.25%20AM.png)
I typed in *test* into the search box to observe how the application behaves. There seems to be a `search` query parameter:
![Screenshot 2024-05-14 at 9.35.44 AM](images/Screenshot%202024-05-14%20at%209.35.44%20AM.png)
I decided to open the developer tools and see if I could check where my test string was input:
![Screenshot 2024-05-14 at 9.42.08 AM](images/Screenshot%202024-05-14%20at%209.42.08%20AM.png)
I then search for the `<script>` tag to see if there was any code that parses user controlled input, to identify any potential sinks. I found the following script:
![Screenshot 2024-05-14 at 9.44.42 AM](images/Screenshot%202024-05-14%20at%209.44.42%20AM.png)
This scripts uses `document.write` to output the corresponding image to the query parameter value if the query parameter value is found. The `query` parameter in the `document.write` method is encapsulated with quotations , so i have to break out of the `img` tags in order to execute my script. I injected the following into the search box:
`'"><script>alert("XSS")</script>` : the `'">` closes out the `img` tag with an empty string and allows execution of the `alert()` function in the injected script. 
This results in the following pop-up, which solves the lab:
![Screenshot 2024-05-14 at 10.05.29 AM](images/Screenshot%202024-05-14%20at%2010.05.29%20AM.png)


