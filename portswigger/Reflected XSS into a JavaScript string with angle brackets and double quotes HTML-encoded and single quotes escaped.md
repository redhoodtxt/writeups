*This lab contains a reflected cross-site scripting vulnerability in the search query tracking functionality where angle brackets and double are HTML encoded and single quotes are escaped.
To solve this lab, perform a cross-site scripting attack that breaks out of the JavaScript string and calls the alert function.*

It says that angle brackets and double quotes are HTML encoded, so I shall try to parse javascript directly. For the string terminator `'` I cannot do so unless I negate the escape functionality. This can be done by adding a `\` to before my payload. I have to nullify the `'` at the end of the string literal, so I added the comment symbol. 
In the end, my payload will look like this:
`\';alert(1);//` 
![[Screenshot 2024-05-16 at 3.44.13 PM.png]]
