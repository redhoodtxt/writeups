 *This lab has user account page that contains the current user's existing password, pre-filled in a masked input. To solve the lab, retrieve the administrator's password, then use it to delete the user carlos. You can log in to your own account using the following credentials: wiener:peter*

Logged with the given credentials: 
![user id controlled by request param with password disclosure](images/user%20id%20controlled%20by%20request%20param%20with%20password%20disclosure.png)

Noticed that the request had a id parameter and the password was disclosed upon logging in. 

Changed the id parameter to *administrator* and was greeted with the following when passing it through Burp Repeater: 
```Burp 
<input required type="hidden" name="csrf" value="CltR2BAzrJyaYiqA4N5GkZkJWUw3nYAd">
<input required type=password name=password value='qmz0u8gyufqdp7xtrkk7'/>
<button class='button' type='submit'> Update password 
```
I copied the password and tried to log in as *administrator*. 

Log in was successful and I managed to delete *carlos*!





