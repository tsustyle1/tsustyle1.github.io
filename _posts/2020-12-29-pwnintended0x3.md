---
title: Pwn Intended 0x3
date: 2020-12-29
excerpt: "'Pwn Intended 0x3' was a challenge in the Pwn category of csictf 2020"
classes: wide
categories: csictf2020
tags:
  - csictf2020
  - pwn
  - buffer-overflow
  - bof
  - radare2
  - python
  - pwntools
---


![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/0.png)


Same thing as Pwn intended 0x2, but this time our destination isn't as visible



Start by analyzing the binary  

![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/1.png)


![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/2.png)


Nothing interesting in main. We did notice sym.flag, let's check that out



![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/3.png)


That's what we want. So it looks like we'll want to jump to 0x004011ce



Same as 0x2, find your padding using python and dmesg.   

![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/4.png)
![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/5.png)


We can see that we start leaking in at 41, so we'll use 40 for padding.



Script:



![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/6.png)


![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x3/7.png)
