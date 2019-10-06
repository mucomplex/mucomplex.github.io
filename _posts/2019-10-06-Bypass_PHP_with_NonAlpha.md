---
title: Bypass with PHP non-alpha encoder 
layout: post
author: mucomplex
description: This really useful when you encounter IDS/IPS prevention which need to bypass php code execution
---

In this tutorial I will cover PHP non-alpha encoder. I will show some basic concept first before we going deeper which may couse brain damage. muehehe <br>

A 	| B 	| 	XOR A&B
--------|-------|-------------------
0       | 0     |          0
1       | 0     |          1
0       | 1     |          1
1       | 1     |          0

so if 'A' xor 'A' should be 0. as example below: <br>
![Image 1](/images/PHP_Non-Alpha/Selection_001.png)<br><br>

now lets try 'A' xor '1' : <br>
![Image 2](/images/PHP_Non-Alpha/Selection_002.png)<br><br>

Wait what?.. how it can be 'p' ? .. what's the logic there?.. Okay,okay.. im going back to basic.<br>
![Image 3](/images/PHP_Non-Alpha/ascii.gif)<br><br>

By opening online calculator <br>
![Image 4](/images/PHP_Non-Alpha/Selection_003.png)<br><br>
In hex, 'A' is '0x41' and '1' is '0x31' , it is not really 0x01. So after xor the value, it get '0x70' which may be the alphabet of 'p' in ascii table <br>

Okay now, what is non-alpha?<br>
**Non-alphanumeric characters that are considered to be symbols are also treated as white space.** <br>
The question is?.. can non-alpha be construct to become strings?.. asnwer: Yes!! <br>

Okay lets take a look again. in hex table, I will use hex 0x20 to 0x40 and 0x7B until 0x7E, so it is not in alphabet range. so with this combination I try to construct a string <br>
![Image 5](/images/PHP_Non-Alpha/Selection_004.png)<br><br>

You have the basic concept now. Lets *fireup* our php cli (I will use php7.x).As we know variable declaration in most programming language accept a-z,A-Z,0-9 and underscore.
I will use underscore as my variable.<br>
First command I use to declare my variables '$\_;'.It will contain undefine variable, which we may assume as 'Null' or '0'.<br>
2nd, I try to increase the '$\_;' by append '++' at the end ($\_++;).Result will be numeric '1' <br>
3rd, by concate string and number, php will take first parameter as its type. ''.$\_ is string '1' . I try to xor again with 'A', it gives 'p'. I hope it is clear. <br>
![Image 6](/images/PHP_Non-Alpha/Selection_005.png)<br><br>

So let construct our string. but lazy?.. okay I made some tool for you, and study the code.<br>
[PHP\_alphanumeric\_encoder](https://github.com/mucomplex/PHP_alphanumeric_encoder) <br>

What is python argumentparser? and how to declare it?<br>
**The argparse module makes it easy to write user-friendly command-line interfaces. The program defines what arguments it requires, and argparse will figure out how to parse those out of sys.argv. The argparse module also automatically generates help and usage messages and issues errors when users give the program invalid arguments.** <br>

![Image 7](/images/PHP_Non-Alpha/Selection_006.png)<br><br>

Then I initialize php\_encoder class with 3 arguments which is payload,method and badchar. I also create symbolic\_list by using string.digits + string.printable[62:94] . <br>
Finally I create list of 'xor' and 'or' non-alpha to be store. <br>

![Image 8](/images/PHP_Non-Alpha/Selection_007.png)<br><br>

Below is function replacing badchar with ''. <br>
![Image 9](/images/PHP_Non-Alpha/Selection_008.png)<br><br>
php\_encoder is check: <br>
1. check if successfully encode all payload character.
2. iteration of xor non-apha and non-alpha.
3. if payload contain non-alpha.It directly pickup the non-alpha character.
4. else it will 'xor' and check if match, it append to the list.
![Image 10](/images/PHP_Non-Alpha/Selection_009.png)<br><br>

if you look at the code, there is another logic that I use. which is 'or' encoder. you may figure out this your self. <br>
Let test the code: <br>
![Image 11](/images/PHP_Non-Alpha/Selection_010.png)<br><br>
![Image 12](/images/PHP_Non-Alpha/Selection_011.png)<br><br>

if you look at echo $\_\_($\_);  it actually same as echo shell\_exec('whoami'). <br>
