---
layout: post
title: Sneaky security vulnerability to watch out for while developing server side OAuth2.0a
description: ""
category: articles
tags: [oauth2.0, security, vulnerability, oauth2.0a]
comments: true
---

Timing attack
=============
This attack is quite common and is applicable to every situation where user send certain information to the server, and it needs to verify this info by matching it to the information stored in server, or via any cryptographic algorithm whose execution time directly depend upon the input data.

This attack is dependent upon implementation of OAuth2.0, and not the protocol itself.

Timing attack can be used in many ways in Oauth2.0 process. I am giving here example of one of the simplest scenario.


Example
-------
In the server side OAuth2.0a process, the last call is to exchange authorisation code
for an access token. On server side, code will first verify the authorisation code, and then compare received client secret to the stored client secret.

Now, Attacker wants to gain access to this server as this client. She knows the client id, but does not know authorisation code and client secret. 

In this case, timing attack would work as follows:

* Attacker sends request using valid client id. And authorisation code and client secret are some random string. Attacker receives the response and measure the time required for that response.

* Now, as you know a standard comparison routine in most programming language is implemented in such a fashion that, they check two byte sequence byte-by-byte and return false, immediately when it found different byte.

* The key concept here is that for **typical string comparision routine the time required to execute is propotional to the position of the first non-matching byte from start of the byte sequence**.

* So, Now all attacker needs to do is change first byte again and again until the time to return error response slightly increases or decreases (if she have used correct byte in first time, time will decrease otherwise it will increase.) After verifying that, she just needs to keep that byte as it is, and change the next byte. This process is continued for rest of the bytes.

One aspect of this attack, that makes it dangerous is that, we don't even need to brute force the code and secret anymore. We can just measure time, and predict that whether current byte is valid or not. This can also be easily automated.


Prevention
----------
* **Use constant time compare functions:** Nowadays, many programming language provide library function that uses constant time to compare two byte sequence, instead of returning decision immediately whenever wrong byte appears.

* **Time-out authorisation code:** Authorisation code should time-out after some reasonable time limit (from 5 minutes to 45 minutes.)


Further Information
-------------------
* [Wikipedia](https://en.wikipedia.org/wiki/Timing_attack)





 



