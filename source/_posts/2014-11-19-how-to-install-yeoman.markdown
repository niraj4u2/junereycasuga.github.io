---
layout: post
title: "How to install Yeoman"
date: 2014-11-19 20:42:06 +0800
comments: true
categories: [yeoman]
---
We used Yeoman from the previous blog I wrote on working with AngularJS. But the problem is, I haven't included there how to install Yeoman. So this is the post you need to read in order to install Yeoman.

##Node.js

To install Yeoman, you must first have Node.js installed on your machine. For Windows users, you can download the installer from [here](http://nodejs.org/download/). And for those who are using Mac OS X or Linux, I prefer using NVM (Node Version Manager). Why? Because it lets you switch from different versions of Node.js at ease. There are 2 ways on how to install NVM, through cURL or through Wget.

To install NVM through cURL:
{% codeblock %}
curl https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
{% endcodeblock %}

To isntall NVM through Wget:
{% codeblock %}
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
{% endcodeblock %}

These scripts clones the NVM repository from Github to `/.nvm` directory and adds the source line to your profile (`/.bash_profile` or `/.profile`).

Once you have installed NVM, you can now use it for installing Node.js. To download, compile and install the latest 0.10.x version of Node.js, do this:
{% codeblock %}
nvm install 0.10
{% endcodeblock %}

And you can now use the Node.js version you just installed by running:
{% codeblock %}
nvm use 0.10
{% endcodeblock %}

##Yeoman
Now that we have Node.js installed on our machine, we are now ready to install Yeoman. Yeoman is using 3 core tools. These core tools are composed by Yo, Grunt, and Bower. So we will install them one by one through NPM (Node Packaged Modules) which came with Node.js when we installed it.

###Yo
Yo is the tool to use for running Yeoman generators. To install it, just run:
{% codeblock %}
npm install -g yo
{% endcodeblock %}

###Grunt
Grunt is the task-manager. To install it, just run:
{% codeblock %}
npm install -g grunt-cli
{% endcodeblock %}

###Bower
Bower is a package manager. To install it, just run:
{% codeblock %}
npm install -g bower
{% endcodeblock %}

##Conclsion
We now have the core tools needed for Yeoman to work, but there is one more thing we need to do. That is to install the generator we want to use. If you want to create a basic webapp, you just need to run `npm install -g generator-webapp` or if you want to work on AngularJS, just run `npm install -g generator-angular`.

We now have all the things needed, and you can now kickstart your project by running `yo webapp` or `yo angular`.
