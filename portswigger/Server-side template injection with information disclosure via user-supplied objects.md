*This lab is vulnerable to server-side template injection due to the way an object is being passed into the template. This vulnerability can be exploited to access sensitive data.
To solve the lab, steal and submit the framework's secret key.
You can log in to your own account using the following credentials:
`content-manager:C0nt3ntM4n4g3r`*

Was able to edit the template after clicking on a product:
![[Screenshot 2024-06-03 at 3.43.09 PM.png]]
Tried to check for SSTI vulnerability:
Injected `${{<%[%'"}}%\.` into the template to receive the following error;
![[Screenshot 2024-06-03 at 3.45.12 PM.png]]
Looks like the template used is `Django`. Let's review the documentation to find a relevant payload that follows the syntax
I found the following payload worked, indicating that the secret key was hard coded into the `settings.py` file:
`{{settings.SECRET_KEY}}`. 
This output the secret key:
![[Screenshot 2024-06-03 at 3.57.49 PM.png]]
