---
title: GI Joe
date: 2020-12-29
excerpt: "'GI Joe' was a challenge in the Web category of Hacktivitycon"
classes: wide
categories: Hacktivitycon2020
tags:
  - hacktivitycon
  - cgi
  - CVE-2012-1823
  - php
  - metasploit
---

![img](/assets/images/ctf/hacktivitycon-web-gijoe/0.png)


![img](/assets/images/ctf/hacktivitycon-web-gijoe/1.png)


See GI Joe? CGI?



`jh2i.com:50008/cgi-bin/`



![img](/assets/images/ctf/hacktivitycon-web-gijoe/2.png)


Doing some enumeration lead me to:



`jh2i.com:50008/?-s`



Which allows grabbing of the source code in older versions of PHP



![img](/assets/images/ctf/hacktivitycon-web-gijoe/3.png)


CVE-2012-1823



[https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2012-1823](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2012-1823)



There's a metasploit module to speed up this process



![img](/assets/images/ctf/hacktivitycon-web-gijoe/4.png)


![img](/assets/images/ctf/hacktivitycon-web-gijoe/5.png)
