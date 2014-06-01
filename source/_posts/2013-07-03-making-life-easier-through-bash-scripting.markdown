---
layout: post
title: "Making life easier through Bash scripting"
date: 2013-07-03 23:36
comments: true
categories: [linux, bash, scripting]
author: Junerey Casuga
---
{% img /images/bash_scripting/bash-fb.png 800 %}
{% img /images/bash_scripting/bash-google-plus.png 800 %}

In the past few days, some of my friends and colleagues saw my cover photo from my [Facebook](https://facebook.com/kaj26kai) and [Google+](https://plus.google.com/105091722637731618991) and asked me, "What is #!/bin/bash?". That's why I came up to an idea on writing about Bash or Shell scripting. This will talk about how bash will help a typical Linux user. I won't be tackling any programming using bash.

<!--more-->

Shell scripting or Bash scripting is commonly used by Linux users. It is actually useful for making your task easier. Well, not actually easier but faster. In this post, I will show you how bash scripting could help you on speeding up a task do you always do.

###The Problem

Let's say you got a freshly installed Linux operating system on your machine. And in Linux, we(or is it only me?) usually install programs through the terminal. And since you have a freshly installed OS, there's a lot of command you want to run on your terminal to install softwares or programs. And sometimes, it is annoying that you have to type a specific command every after a software is installed.

###The Solution
To make your life easier, we can use shell scripting to run all of those commands with just one command on your terminal.


###Shebang
{% blockquote NetTuts http://net.tutsplus.com/tutorials/other/the-fundamentals-of-bash-scripting/ %}
A <b>Shebang</b> is the combination of hash and an exclamation mark : <b>#!</b>. The program loader will look for the shebang on the first line of script and use the interpreter specified in it.
{% endblockquote %}

A shebang consists the following syntax:
`#!interpreter [parameters]`
The interpreter is the program used to interpret the language used. For bash scripting, we would use `#!/bin/bash`.


###Examples
Let's take the problem above where you are tired of typing a lot of command one after another. So we will use shell scripting to make your task faster. Let's say I had a freshly installed Linux OS on my machine and I want to install programs I usally install on my machine like LAMP. Installing LAMP uses different commands because it will install Apache, MySQL and PHP. Now, let's use bash to run the commands used to install LAMP.

{% codeblock lang:bash %}
#!/bin/bash

sudo apt-get update && sudo apt-get install apache2 && sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt && sudo apt-get install phpmyadmin && sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql && sudo mysql_install_db && sudo /usr/bin/mysql_secure_installation

exit 0
{% endcodeblock %}

And let's save it as `install-lamp.sh`.

To run this specific shell script, open up your terminal and navigate to the directory where you saved `install-lamp.sh`. And run `bash install-lamp.sh`. As you hit enter key, all the commands you've inserted inside the shell script will be run automatically without you typing everytime on software is done installing.

###Very Short Explanation
As you can see, the script basically contains the shebang with the interpreter(bash) and a string of terminal commands linked together using `&&`. This means that we'll run this commands one after another.

###Conclusion
In fact, you can do more than this. You can do a lot of things through shell scripting. Shell scripting is not only for programmers. In fact, even a typical Linux user can use it for speeding up some task. This could be a big help for finishing a task faster. So I would love to say that <b>I <3 #!/bin/bash</b>. :)
