*This lab demonstrates a reflected DOM vulnerability. Reflected DOM vulnerabilities occur when the server-side application processes data from a request and echoes the data in the response. A script on the page then processes the reflected data in an unsafe way, ultimately writing it to a dangerous sink.
To solve this lab, create an injection that calls the alert() function.*

Greeted with a search box:
![Screenshot 2024-05-14 at 3.14.18 PM](images/Screenshot%202024-05-14%20at%203.14.18%20PM.png)
I opened my developer console and input a 'test' string into the search box. I noticed the following function in the code:
![Screenshot 2024-05-14 at 4.29.36 PM](images/Screenshot%202024-05-14%20at%204.29.36%20PM.png)
I couldn't find this expression anywhere else in the code, so I checked the *searchResults.js* in *Debugger->Sources*
I found the function definition for `search`, where there was a potential sink in `eval()`.
![Screenshot 2024-05-14 at 4.32.33 PM](images/Screenshot%202024-05-14%20at%204.32.33%20PM.png)
I saw that there was a `responseText` concatenated to the string parsed for eval, so I deduced that this must be from the server response when submitting the string in the search box:
![Screenshot 2024-05-14 at 4.35.58 PM](images/Screenshot%202024-05-14%20at%204.35.58%20PM.png)
This shows that the string passed into the search box is returned in the response, where the data is then passed into the `eval` function in `search` , which is a potential sink. 

I then tried to input the standard payload, but it did not work. After trying multiple payloads, I noticed that the JSON response is escaping quotation marks with a `\`, preventing me from closing the double quotes when injecting the payload.

I then tried to add a `\` before a `"` followed by my payload. This would effectively cancel the escaping of the `"`, as when JSON sees the `"` and adds a `\`, there is already an extra `\` included, making it `\\"` which keeps `"`
I suffixed my payload with } to end the JSON response, followed by // to comment out the remaining syntax. 
Before my actual payload, I separated the expressions with a `-` to ensure that the `alert()` function will be properly processed.

In the end, the following should be inserted into the search bar:
``\"`-alert(1)}//`
![Screenshot 2024-05-14 at 4.45.48 PM](images/Screenshot%202024-05-14%20at%204.45.48%20PM.png)
This solved the lab!
