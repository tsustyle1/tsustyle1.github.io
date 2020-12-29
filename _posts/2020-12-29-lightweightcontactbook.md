---
title: Lightweight Contact Book
date: 2020-12-29
excerpt: "'Lightweight Contact Book' was a challenge in the Web category of Hacktivitycon"
classes: wide
categories: Hacktivitycon2020
tags:
  - hacktivitycon
  - LDAP
  - injection
  - web
  - python
---


![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/0.png)


![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/1.png)


While enumerating this I found that you can dump the database using '*', which means it's probably LDAP



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/2.png)


To confirm, we can try some injection



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/3.png)


LDAP indeed. So how do we exploit this? Well, there was a hint when trying to recover the administrator's account



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/4.png)


So there's a description field in the database that we haven't uncovered yet. Fortunately, we can use wildcards to try and uncover the password from that field



It works like this



administrator)(description=a*



if the value in the description field starts with 'a', then it will return the public data. If not, then it wont. So we can bruteforce this.



Correct:



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/5.png)


Incorrect:



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/6.png)


You could go through this by hand, checking each character and eventually get it, or you can script it. I took the latter option



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/7.png)


![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/8.png)


Log in with administrator:very\_secure\_hacktivity_pass



![img](/assets/images/ctf/hacktivitycon-web-lightweightcontactbook/9.png)
