*This lab is vulnerable to server-side template injection. To solve the lab, identify the template engine and use the documentation to work out how to execute arbitrary code, then delete the morale.txt file from Carlos's home directory.
You can log in to your own account using the following credentials: `content-manager:C0nt3ntM4n4g3r`*

Came across this when I clicked on *Edit Template* after clicking on a product:
![[Screenshot 2024-06-03 at 2.15.44 PM.png]]
I tried to replace one of the template syntax with a non-existent code to trigger an error response that code give me insights on what template is being used:
![[Screenshot 2024-06-03 at 2.24.32 PM.png]]
This gave me the following error response:
![[Screenshot 2024-06-03 at 2.25.31 PM.png]]
I'm guessing that the template used here is `Freemarker`. Let's search for the proper syntax for this and find a relevant payload. 
I got the following from portswigger's website and modified it to delete `morale.txt`:
`<#assign ex="freemarker.template.utility.Execute"?new()> ${ ex("rm /home/carlos/morale.txt") }`
This solved the lab:
![[Screenshot 2024-06-03 at 2.40.13 PM.png]]
