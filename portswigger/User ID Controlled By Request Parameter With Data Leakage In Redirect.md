*This lab contains an access control vulnerability where sensitive information is leaked in the body of a redirect response. To solve the lab, obtain the API key for the user carlos and submit it as the solution. You can log in to your own account using the following credentials: wiener:peter*

Logged in with the given credentials and tried to change the user ID in the request parameter to *carlos*. This redirects the page to the login page, so i decided to intercept the request when redirecting : 

```URL 
<div id=account-content>
	<p>Your username is: carlos</p>
<div>Your API Key is: o2G6VNlgffqDA5xXfcscAtUVL8MkOeaf</div>
```

Done!
