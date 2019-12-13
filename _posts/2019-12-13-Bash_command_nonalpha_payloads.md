---
title: bash command nonalpha payload
layout: post
author: mucomplex
description:This useful when you encounter IDS/IPS prevention which need to bypass command execution.
---

This might your first introduce to bash non-alpha payload,I can bet no better explaination and article for this topic than me :D . This might change your perspective to bash scripting and how to abused it.<br>

I wonder not much people research about this, but I have done my own research to upgrade your hacking skill :D <br>

Let me introduce you list of special bash parameter used in Unix.
![Image 1](/images/Bypass_trick/bash_nonalpha/Selection_001.png)<br><br>

Now,you need to know how to initialize function in single line cmd shell: <br>
function\_name () { commands; } <br>

As you know declaration of function variable can be start by upper and lower case alphabet, other than that is <b>underscore</b> <br>
eg: __="this is my variable"<br>
input : echo $__ <br>
result: this is my variable <br>

Now let's going deep.<br>

\_\_\_\_()    {    \_\_=$#;}; -- This part we declare function which obtain number of argument return ($#) and assign as \_\_ <br>
\_\_\_\_    $#;		-- This we trigger the function and give one parameter to it. <br>
echo $\_\_ 		-- you will get one(1) based on function assignment. <br>

![Image 1](/images/Bypass_trick/bash_nonalpha/Selection_001.png)<br><br>





Reference link: <br>
https://javarevisited.blogspot.com/2011/06/special-bash-parameters-in-script-linux.html <br>
https://linuxize.com/post/bash-functions/ <br>


