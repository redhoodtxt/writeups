*This lab has a logic flaw in its purchasing workflow. To solve the lab, exploit this flaw to buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter*

Signed up for the newsletter using my exploit server email to receive a `SIGNUP30` coupon like before and logged into my account with the given credentials. I noticed that I had the option of redeeming gift cards in *My account*:
![[Screenshot 2024-05-12 at 9.03.57 PM.png]]
I tried going through the whole purchasing workflow for buying a gift card, coming across the following:
![[Screenshot 2024-05-12 at 9.07.01 PM.png]]
Applying the coupon, I get the gift card code in my email, which I can use to increase my store credit to $103 dollars.
![[Screenshot 2024-05-12 at 9.09.24 PM.png]]
![[Screenshot 2024-05-12 at 9.09.57 PM.png]]

As I am able to increase my store credit by exploiting this flaw, I decided to automate this series of requests using *Macros* on Burp. 

Under *Settings->Sessions->Session Handling Rules->Scope*, I added a new rule where I would "Include all URLs" 
![[Screenshot 2024-05-12 at 9.19.18 PM.png]]
and under *Details* I would "Run a macro":
![[Screenshot 2024-05-12 at 9.20.53 PM.png]]
Highlighted and filtered the following requests in the *Macro Recorder*:
![[Screenshot 2024-05-12 at 9.28.45 PM.png]]
*Add gift card to cart->apply coupon->checkout with gift-card with coupon->get the confirmation with gift cart code->apply coupon in account to increase credit*
Clicked on the 4th response to *Configure item* so that there I can add a custom parameter for the gift card to be applied in request 5:
![[Screenshot 2024-05-12 at 9.30.24 PM.png]]
![[Screenshot 2024-05-12 at 9.32.09 PM.png]]
![[Screenshot 2024-05-12 at 9.33.14 PM.png]]
Configured the 5th request to receive the coupon parameter value from the 4th response:
![[Screenshot 2024-05-12 at 9.36.50 PM.png]]
Testing the macro was successful:
![[Screenshot 2024-05-12 at 10.01.11 PM.png]]
I sent the `/my-account` request to *Intruder* and used 412 null payloads, as that was the required amount of payloads to generate enough store credit. I also set the maximum concurrent requests to be 1 as the macro requests had to be in order. 

After awhile, I was able to get enough store credits to buy the jacket and solve the lab!
![[Screenshot 2024-05-12 at 11.03.11 PM.png]]
