*This lab demonstrates a stored DOM vulnerability in the blog comment functionality. To solve this lab, exploit this vulnerability to call the alert() function.*

Accessed the comment function under one of the blogs and posted the comment, observing the output in *Proxy*. 
I noticed that the response stores the comments in `JSON` 
![[Screenshot 2024-05-14 at 5.27.10 PM.png]]
When accessing the blog again, it loads the comments from the following URL:
![[Screenshot 2024-05-14 at 5.29.13 PM.png]]
I checked out the page using *Debugger->Sources* in the developer console. 
I looked for `innerHTML` as it is a potential sink for stored DOM XSS, and found the following function:
![[Screenshot 2024-05-14 at 5.38.46 PM 1.png]]
I noticed that there is a `newInnnerHTML` variable that incorporates an `escapeHTML` function. I decided to take a look at the `escapeHTML` function:
![[Screenshot 2024-05-14 at 5.44.12 PM.png]]
It seems like that the script passes the JSON response into the `escapeHTML` function where it prevents the use of angle brackets.
However, the replacement only replaces the first instance of angle brackets, not the rest. 
Hence, I inserted the following payload: 
`<><iframe src = javascript:alert(1)>`
Note that that `javascript:alert(1)` does not work for `<img src= >` (this got patched bruh fml) for `<img>` tag use `<img src = 1 onerror=alert(1)`
This will result following successful solve of the lab!
![[Screenshot 2024-05-14 at 6.15.34 PM.png]]
