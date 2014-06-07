---
layout: post
title: "Getting Started with Ruby"
description: "This is a very elegant and wonderful stone, I mean programming language"
date: 2013-09-16 21:26
comments: true
categories: [ruby] 
author: Junerey Casuga
---
As promised, I will be showing you how to code Ruby. But don't expect too much. I'll just show you the very basic of it. So without further adieu, here it is.

<!--more-->

###Ruby Installation
First of all, you must have Ruby installed on your machine to get started with Ruby development. There are two ways to install Ruby on your machine. It is by using rbenv or rvm. Both of them are used to manage Ruby versions on your machine. But on this article I will show you how to use rvm to install Ruby on a Linux environment. It will be easy and quick.

Let's install first RVM by running this command on your terminal:
{% codeblock %}
curl -L https://get.rvm.io | bash -s  stable --ruby
{% endcodeblock %}

What this does is it downloads Ruby and installs the latest stable Ruby version. After installing Ruby on your system, run `rvm rubygems latest` to get the latest gems.

For installing Ruby on your Windows machine, you can just download the installer from the [Ruby website](https://www.ruby-lang.org/en/). Once you have installed Ruby on your Windows machine, you can check if it is working by tping this command on your command prompt:

{% codeblock %}
$ ruby -v
{% endcodeblock %}

This should show the version of your Ruby.

###The IRB
IRB or Interactive Ruby is like a command line for Ruby. You can type Ruby command and it will return a value of the line of code you've entered. To try IRB, you can just type `irb` on your terminal or command prompt. Once you've done that, try out some of these lines of codes. <small>Note: The '$' sign represents the IRB prompt</small>

{% codeblock %}
$ 1 + 2
=> 3
{% endcodeblock %}

Easy right? Now let's try to output a string value.

{% codeblock %}
$ puts "Hello World"
Hello World
=> nil
{% endcodeblock %}

Cool! It outputs the phrase "Hello World" and it returned a <i>nil</i> value. <i>nil</i> means null for Ruby. Alright, let's move on. Let's go deeper. How about we write a function?

{% codeblock %}
$ def greet
$   return "Hello World"
$ end
=> nil
$ greet
=> "Hello World"
{% endcodeblock %}

As you can see, we made a function named as "greet" which returns the "Hello World" phrase when it was called.

###Conclusion
Alright! I won't go deeper with this now. We've already learned how to install Ruby on your machine and we also learned how to use IRB for exploring Ruby. It's now your time to find out more what Ruby can do. Thanks for reading!
