*This lab involves a front-end and back-end server, and the two servers handle duplicate HTTP request headers in different ways. The front-end server rejects requests that aren't using the GET or POST method.
To solve the lab, smuggle a request to the back-end server, so that the next request processed by the back-end server appears to use the method GPOST.*

Used the *Smuggle Probe* function in *HTTP Request Smuggler* to scan for request smuggling vulnerabilities. While that was happening, I manually tested for the vulnerability using the [[Notes v1.1#HTTP Request Smuggling Methodology]]. Sent the request and received the `200 OK` response. I then tried the 2 different payloads outlined in [[Notes v1.1#HTTP Request Smuggling Methodology]](see flowchart of payloads)
The following payload gave a error with rejection:
![[Screenshot 2024-06-12 at 3.53.46 PM.png]]
This means that the site is vulnerable to either a `TE.TE` or `TE.CL`. 

I then tried the following payload which gave the this response:![[Screenshot 2024-06-12 at 3.58.36 PM.png]]
As I received a `200 OK` this confirms that it is a `TE.TE` vulnerability.
I then tried all the payloads listed to obfuscate the `Transfer-Encoding` as seen in [[Notes v1.1#`TE.TE` Obfuscating TE Header]], and saw that using:
```
Transfer-Encoding: chunked
Transfer-Encoding: x
```
gave me a timeout:
![[Screenshot 2024-06-12 at 4.18.58 PM 2.png]]
This means that the front-end is more lenient towards processing the `Transfer-Encoding` and processes `Transfer-Encoding: chunked` instead of the arbitrary one, dropping the `X`. The back-end is stricter, seeing that one of the headers is invalid, and chooses to use `Content-Length` to process the request. Since the specified `Content-Length` is 6 and there are now 5 bytes, it waits for the 6th byte until timeout. 
![[Screenshot 2024-06-12 at 4.26.13 PM.png]]
The next goal is the following:
![[Screenshot 2024-06-12 at 4.43.07 PM.png]]
I modified my attack request to be identical to the above. I then sent the initial homepage request to the *Repeater*, modifying to be identical to the above. 

*The normal request:*
![[Screenshot 2024-06-12 at 4.48.20 PM.png]]
The attack request:
![[Screenshot 2024-06-12 at 4.58.28 PM.png]]
I sent the attack request first, received a `200 OK` response, and then submitted the normal request to receive the following response:
![[Screenshot 2024-06-12 at 4.59.34 PM.png]]
Modified the attack request as seen below. You can then choose to send the attack request first followed by the normal request, or send the attack request twice. I opted for the latter, and got the following successful error message:
![[Screenshot 2024-06-12 at 5.08.10 PM.png]]
