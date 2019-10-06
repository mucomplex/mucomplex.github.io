---
title: Bypass with PHP non-alpha encoder 
layout: post
author: mucomplex
description: This really useful when you encounter IDS/IPS prevention which need to bypass php code execution
---

In this tutorial I will cover PHP non-alpha encoder. I will show some basic concept first before we going deeper which may couse brain damage. muehehe <br><br>

A 	| B 	| 	XOR A&B
--------|-------|-------------------
0       | 0     |          0
1       | 0     |          1
0       | 1     |          1
1       | 1     |          0

so if 'A' xor 'A' should be 0. as example below: <br><br>
![Image 1](/images/PHP_Non-Alpha/Selection_001.png)<br><br>

now lets try 'A' xor '1' : <br><br>
![Image 2](/images/PHP_Non-Alpha/Selection_002.png)<br><br>

Wait what?.. how it can be 'p' ? .. what's the logic there?.. Okay,okay.. im going back to basic.<br><br>
![Image 3](/images/PHP_Non-Alpha/ascii.gif)<br><br>

By opening online calculator <br>
![Image 4](/images/PHP_Non-Alpha/Selection_003.png)<br><br>
In hex, 'A' is '0x41' and '1' is '0x31' , it is not really 0x01. So after xor the value, it get '0x70' which may be the alphabet of 'p' in ascii table <br><br>

Okay now, what is non-alpha?<br><br>
**Non-alphanumeric characters that are considered to be symbols are also treated as white space.** <br><br>
The question is?.. can non-alpha be construct to become strings?.. asnwer: Yes!! <br><br>

Okay lets take a look again. in hex table, I will use hex 0x20 to 0x40 and 0x7B until 0x7E, so it is not in alphabet range. so with this combination I try to construct a string <br>
![Image 5](/images/PHP_Non-Alpha/Selection_004.png)<br><br>

You have the basic concept now. Lets *fireup* our php cli (I will use php7.x).As we know variable declaration in most programming language accept a-z,A-Z,0-9 and underscore.
I will use underscore as my variable.<br><br>
First command I use to declare my variables '$\_;'.It will contain undefine variable, which we may assume as 'Null' or '0'.<br>
2nd, I try to increase the '$\_;' by append '++' at the end ($\_++;).Result will be numeric '1' <br>
3rd, by concate string and number, php will take first parameter as its type. ''.$\_ is string '1' . I try to xor again with 'A', it gives 'p'. I hope it is clear. <br><br>
![Image 6](/images/PHP_Non-Alpha/Selection_005.png)<br><br>

