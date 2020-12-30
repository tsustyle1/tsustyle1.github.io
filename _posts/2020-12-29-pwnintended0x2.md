---
title: Pwn Intended 0x2
date: 2020-12-29
excerpt: "'Pwn Intended 0x2' was a challenge in the Pwn category of csictf 2020"
classes: wide
categories: csictf2020
tags:
  - csictf2020
  - pwn
  - buffer-overflow
  - bof
  - python
  - pwntools
---

![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/0.png)


Let's analyze the binary



![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/1.png)


![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/2.png)


We can see that it's calling gets and we can see where we want to end up. Looks like we want to overflow and set the instruction pointer to that address. Let's do it.



First, let's see if we can find how many junk characters we need to send for padding



Using python and dmesg, we can send different lengths and check where exactly the segfault is occuring



![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/3.png)

![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/4.png)


So at 57, we can start to see 41 (A) leaking in. Let's use 56 as our padding then.  

So now we know both the address we want to jump to (0x004011d3) and the padding required (56).  

Let's write a script using python and pwntools.



![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/5.png)


![img](/assets/images/ctf/csictf2020-pwn-pwnintended0x2/6.png)
