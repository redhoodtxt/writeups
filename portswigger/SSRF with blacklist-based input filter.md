*This lab has a stock check feature which fetches data from an internal system.
To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.
The developer has deployed two weak anti-SSRF defenses that you will need to bypass.*

Checked stock for one of the items. Sent the request to the *Repeater* and modified the parameter `stockApi` to access `/admin`, only to be met with the following error:
![[Screenshot 2024-05-27 at 11.50.54 AM.png]]
Did some alternative IP representation and obfuscated the `a` in `admin` with URL encoding:
![[Screenshot 2024-05-27 at 12.04.02 PM.png]]
Navigated to the URL to delete carlos:
![[Screenshot 2024-05-27 at 12.05.57 PM.png]]
