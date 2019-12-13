---
title: Space Bypass,Concatenation
layout: post
author: mucomplex
description: This useful when you encounter IDS/IPS prevention which need to bypass command execution
---

Today I will show some trick to bypass when you want to invade the target machine<br>
## Space Bypass <br>
Curly braces the command and argument. eg: {command,arg1,arg2,..} <br><br>
The output will result as image 1 <br><br>
![Image 1](/images/Bypass_trick/Space_Bypass/Selection_001.png)<br><br>
Define _${IFS}_ which mean "internal field separator" <br><br>
![Image 2](/images/Bypass_trick/Space_Bypass/Selection_002.png)<br><br>
#### mysql space bypass <br>
with "/**/" <br>
![Image 3](/images/Bypass_trick/Space_Bypass/Selection_003.png)<br><br>
with "+" <br>
![Image 4](/images/Bypass_trick/Space_Bypass/Selection_004.png)<br><br>


## Concatenation <br>
? Operator , this will subtitute alphabet as single wildcard. <br>
![Image 1](/images/Bypass_trick/Concatenation/Selection_001.png)<br><br>
Quote <br>
![Image 2](/images/Bypass_trick/Concatenation/Selection_002.png)<br><br>
Uninitialized variables <br>
![Image 3](/images/Bypass_trick/Concatenation/Selection_003.png)<br><br>
WildCard <br>
![Image 4](/images/Bypass_trick/Concatenation/Selection_004.png)<br><br>
