*This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket".
You can log in to your own account using the following credentials: wiener:peter*

Logged in and noticed I had $100 dollars in my account. I decided to place an order for the jacket into my cart, tracking the requests *Proxy*.

Sifting through the requests, there were no parameters where there were any `price` fields to manipulate. However, there was a quantity field that we could manipulate. 
![Screenshot 2024-05-09 at 5.21.06 PM](images/Screenshot%202024-05-09%20at%205.21.06%20PM.png)
We could try and trying a abnormally large quantity and see how the application responds. 

I forwarded the request to *Intruder* to set the insertion point and use the *Numbers* payload, where I set the limit to 150:
![Screenshot 2024-05-09 at 5.24.36 PM](images/Screenshot%202024-05-09%20at%205.24.36%20PM.png)
![Screenshot 2024-05-09 at 5.24.55 PM](images/Screenshot%202024-05-09%20at%205.24.55%20PM.png)
From the results below, the has a limit of 100 of the item being added at a time:
![Screenshot 2024-05-09 at 5.28.17 PM](images/Screenshot%202024-05-09%20at%205.28.17%20PM.png)
We can then remove the payload markers:![Screenshot 2024-05-09 at 5.33.04 PM](images/Screenshot%202024-05-09%20at%205.33.04%20PM.png)

use null payloads and continue the process indefinitely until we see the application response differently.:
![Screenshot 2024-05-09 at 5.33.23 PM](images/Screenshot%202024-05-09%20at%205.33.23%20PM.png)
We also have to set the number of concurrent requests to 1:
![Screenshot 2024-05-09 at 5.33.54 PM](images/Screenshot%202024-05-09%20at%205.33.54%20PM.png)
I kept refreshing the website and paused the attack when I saw anything different in the website. 

After awhile, I saw that the total price in the cart dropped to negative!:
![Screenshot 2024-05-09 at 5.36.50 PM](images/Screenshot%202024-05-09%20at%205.36.50%20PM.png)

The goal now is to bring the total price to a value within our store limit. 
I had to figure out the number of jackets to add to bring the price to a positive value. Using math, that number was 14101. 
I then had to figure the number of intruder attacks to perform, which was 14101/99 = 142.

I changed the option under Null payloads to generate 142 payloads:
![Screenshot 2024-05-09 at 5.44.25 PM](images/Screenshot%202024-05-09%20at%205.44.25%20PM.png)
