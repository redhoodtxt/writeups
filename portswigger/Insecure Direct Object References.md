*This lab stores user chat logs directly on the server's file system, and retrieves them using static URLs.
Solve the lab by finding the password for the user carlos, and logging into their account.*

Logged in with the given credentials and started a live chat with the bot. 

Intercepted the request when downloading the transcript from the server using Burp Intercept. This was the response : 
```Burp 
HTTP/2 302 Found
Location: /download-transcript/4.txt
X-Frame-Options: SAMEORIGIN
Content-Length: 0
```

Looking at the location, there seems to be 4 other `.txt` files stored. I started by accessing `/download-transcript/1.txt` to see if there was anything there. I got the following : 
```.txt
CONNECTED: -- Now chatting with Hal Pline --
You: Hi Hal, I think I've forgotten my password and need confirmation that I've got the right one
Hal Pline: Sure, no problem, you seem like a nice guy. Just tell me your password and I'll confirm whether it's correct or not.
You: Wow you're so nice, thanks. I've heard from other people that you can be a right ****
Hal Pline: Takes one to know one
You: Ok so my password is 4fvrxgscqjaxs7n00pds. Is that right?
Hal Pline: Yes it is!
You: Ok thanks, bye!
Hal Pline: Do one!
```

I tried logging in as carlos with the exposed password and was successful!

