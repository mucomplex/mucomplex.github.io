---
title: Bash command nonalpha injection
layout: post
author: mucomplex
description: This useful when you encounter IDS/IPS prevention which need to bypass command execution.
---

This might your first introduce to bash non-alpha payload,I can bet no better explaination and article for this topic than me :D . This might change your perspective to bash scripting and how to abused it.<br>

I wonder not much people research about this, but I have done my own research to upgrade your hacking skill :D <br>

Let me introduce you list of special bash parameter used in Unix.
![Image 01](/images/Bash_Non-Alpha/Selection_0001.png)<br><br>

Now,you need to know how to initialize function in single line cmd shell: <br>
<b>function\_name () { commands; }</b> <br>

As you know declaration of function variable can be start by upper and lower case alphabet, other than that is <b>underscore</b> <br>
eg: <b>\_\_="this is my variable"</b><br>
input : <b>echo $\_\_</b> <br>
result: <b>this is my variable</b> <br>

Now let's going deep.<br>

<b>\_\_\_\_()    {    \_\_=$#;};</b>-- This part we declare function which obtain number of argument return ($#) and assign as \_\_ <br>
<b>\_\_\_\_    $#;		</b>-- This we trigger the function and give one parameter to it. <br>
<b>echo $\_\_ 		        </b>-- you will get one(1) based on function assignment. <br>

![Image 1](/images/Bash_Non-Alpha/Selection_001.png)<br><br>

If you using <b>$-</b> you will get current option flag specifier.So, what we do with this?,This will be our swift knife to success build our payload.I assigned as <b>\_\_\_\_</b><br>
![Image 2](/images/Bash_Non-Alpha/Selection_002.png)<br><br>

Next we will look how to create list of array by encode our \_\_\_\_ with {}.From that, we extract each alphabet. ${\_\_\_\_:index value:size of value} <br>
![Image 3](/images/Bash_Non-Alpha/Selection_003.png)<br><br> 

from example above you know that you have limited character,but what we can do with this?.you see that we can obtain alphabet <b>h,s</b> and <b>i</b>. by manipulating and arrange the value,
we could obtain something like image below. seem familiar right :D. If you remember my previous article about IDS bypass, you possible to subtitute missing alphabet with "<b>?</b>" <br>
![Image 4](/images/Bash_Non-Alpha/Selection_004.png)<br><br> 
we can't use number remember?. So we will use our first trick and replace all number with our non-alpha character <br>
![Image 5](/images/Bash_Non-Alpha/Selection_005.png)<br><br> 

resulting execute this non-alpha payload, you may obtain shell! . Yeah!!! <br>
![Image 6](/images/Bash_Non-Alpha/Selection_006.png)<br><br> 

with all these things together you have complete the payload :D <br>
![Image 7](/images/Bash_Non-Alpha/Selection_007.png)<br><br> 

Now hands-on time!,save it as challenge.py and feed 1st argument with payload. There has various way solution, but you need try hard 1st :D.<br>

<b>import os</b><br>
<b>import sys</b><br>
<b>import re</b><br>
<b>import subprocess</b><br>
<b>value = re.sub(r'[a-zA-Z0-9]','',sys.argv[1])</b><br>
<b>os.system(value)</b><br>


Need something like this advanced? sure can. <b> LiveOverflow!! </b><br>
[https://www.youtube.com/watch?v=6D1LnMj0Yt0&t=198s]https://www.youtube.com/watch?v=6D1LnMj0Yt0&t=198s <br>

Reference link: <br>
[https://javarevisited.blogspot.com/2011/06/special-bash-parameters-in-script-linux.html]https://javarevisited.blogspot.com/2011/06/special-bash-parameters-in-script-linux.html <br>
[https://linuxize.com/post/bash-functions/]https://linuxize.com/post/bash-functions/ <br>
[https://ryanstutorials.net/bash-scripting-tutorial/bash-variables.php]https://ryanstutorials.net/bash-scripting-tutorial/bash-variables.php <br>
[https://bash.cyberciti.biz/guide/Pass_arguments_into_a_function]https://bash.cyberciti.biz/guide/Pass_arguments_into_a_function <br>
[https://stackoverflow.com/questions/42757236/what-does-mean-in-bash]https://stackoverflow.com/questions/42757236/what-does-mean-in-bash <br>
[https://www.modzero.com/modlog/archives/2019/10/04/exploit_wars_ii_-_the_server_strikes_back/index.html]https://www.modzero.com/modlog/archives/2019/10/04/exploit_wars_ii_-_the_server_strikes_back/index.html <br>


