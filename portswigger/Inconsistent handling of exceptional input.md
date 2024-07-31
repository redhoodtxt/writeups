*This lab doesn't adequately validate user input. You can exploit a logic flaw in its account registration process to gain access to administrative functionality. To solve the lab, access the admin panel and delete the user carlos.*

Checked the admin page first: 
![[Screenshot 2024-05-10 at 9.47.33 AM.png]]

I tried checking how the application would respond based on an abnormally long string for an email, and it turns out it truncates the email at roughly 255 characters. I can use this to direct the registration to my exploit server and verify as an admin. 
I generated a long string as such : 
`llkzkdcjkvnazkacdjzxkncjvkzxnfajlkdkkzdkajnfakj7RuagwFAnfpa1lD6OaJQUZxTmsBvGhoFLYo5hhTaJROcV4mEPeWzJBUsNklax0tDIE7oNJhNarL5kGSjRvUgTLHjRkxzU9XMRK9815mwwpuWtQTojwTivZeDq2ED9F4yWVip1rJTqn5d2qWIG0k3sX3jjpgqwQhqorodQJCTcVXvNGxPP3cLlk1kTCpy9F1@dontwannacry.com.exploit-0a87003903d957c0806811820165003b.exploit-server.net`

This will result in the application truncating the email at the `m` of `.com`, registering it as a `dontwannary` user but sending the confirmation email to my exploit server. Registering gave me the following link in my email client:
![[Screenshot 2024-05-10 at 10.15.04 AM.png]]
I clicked on the link and then logged into my account:
![[Screenshot 2024-05-10 at 10.16.00 AM.png]]
Given access to the admin panel, I was able to delete *carlos* and solve the lab.