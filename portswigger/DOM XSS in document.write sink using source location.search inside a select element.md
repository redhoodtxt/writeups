*This lab contains a DOM-based cross-site scripting vulnerability in the stock checker functionality. It uses the JavaScript document.write function, which writes data out to the page. The document.write function is called with data from location.search which you can control using the website URL. The data is enclosed within a select element.
To solve this lab, perform a cross-site scripting attack that breaks out of the select element and calls the alert function.*

Greeted by the following, where I can view products:
![[Screenshot 2024-05-14 at 10.32.28 AM.png]]
I clicked on the 1st product to view the details, greeted with a feature to check stock:
![[Screenshot 2024-05-14 at 10.33.28 AM.png]]
I tried clicking on the feature and viewing the response:
![[Screenshot 2024-05-14 at 10.34.37 AM.png]]
The result appears on the same page, proving that there the checking of stock is executed on the client side. Furthermore, there is a query parameter for `productId`, so there must be some use of DOM methods. 
I opened up the developer tools to view the source. I first searched for `productId`:
![[Screenshot 2024-05-14 at 10.38.24 AM 1.png]]
I then searched for script tags, and came across the following that was below the above screenshot:
![[Screenshot 2024-05-14 at 10.49.10 AM.png]]
This script:
1. creates a list of pre-existing stores
2. creates a new variable `store` to which is assigned a URL parameter `storeID`
3. if the variable `store` exists, it will use the `document.write` function to add to the dropdown list and select that store
4. else, it will output the list `stores` as a dropdown list
I decided to test this by adding the following URL parameter : `&StoreId=2`
![[Screenshot 2024-05-14 at 10.52.51 AM.png]]
I then decided to try to break out of the dropdown list by adding the following as a suffix:
`</option></select>` in front of 2:
![[Screenshot 2024-05-14 at 11.05.43 AM.png]]
I then changed 2 to the following payload, making sure to close the dropdown list:
`</option></select><script>alert(1)<script>` - this stores the script as the `storeId`
This gave the following successful output:
![[Screenshot 2024-05-14 at 11.08.06 AM.png]]
