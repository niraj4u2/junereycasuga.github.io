---
layout: post
title: "What do I install on my machine?"
date: 2013-04-28 18:36
comments: true
categories: [ubuntu, linux, applications, programs, tools]
author: Junerey Casuga 
---
This post is just something that I want to share to you. And this can be also as a reminder and guide for me when I have a freshly installed OS on my machine.

<!--more-->

I am a Linux user. I'm currently running Ubuntu 14.04. I will give you my list of programs, tools, and some applications that I install after installing a fresh OS. I will also show you how to install them. So let's get started.

###LAMP
As we all know, LAMP stands for Linux, Apache, MySQL, and PHP. These are open-source softwares used to make your web server running. Since I am running on Ubuntu, which is a Linux distro, we don't have to take care about it. What we should just install is just the Apache, MySQL, and PHP.

####Apache
To install Apache, just run this line of command in your terminal:

{% codeblock %}
sudo apt-get update
sudo apt-get install apache2
{% endcodeblock %}

That's it. To check if it works, just open your browser and type in <http://127.0.0.1> or `localhost`. It should display "It works!" on the page.

####MySQL
MySQL is basically a database management system. It is where you store data from your web application and retrieve data that is being displayed on your web application.

To install MySQL, run this line of command in your terminal:
{% codeblock %}
sudo apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql
{% endcodeblock %}

After install MySQL, activate it with this command:
{% codeblock %}
sudo mysql_install_db
{% endcodeblock %}

To finalize the installation, run this command:
{% codeblock %}
sudo /usr/bin/mysql_secure_installation
{% endcodeblock %}

A prompt message will ask you a lot of questions. Just answer all of them with Yes.

####PHP
PHP is a server-side scripting language used to build dynamic websites.

To install PHP, run this line of command in your terminal:
{% codeblock %}
sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt
{% endcodeblock %}

Installing LAMP won't install phpMyAdmin yet. To install phpMyAdmin, just run this on your terminal:
{% codeblock %}
sudo apt-get install phpmyadmin
{% endcodeblock %}

That's it! As easy as 1-2-3!

###Sublime Text
Text editors are very essential for all developers. Ubuntu has a pre-installed text editor, Gedit. But I don't like it. That's why I always use Sublime Text as my text text editor.

To install Sublime Text 2, download the `.tar.bz2` file from Sublime Text's [website](http://www.sublimetext.com/2) and extract it by running this command on your terminal:
{% codeblock %}
tar xf Sublime\ Text\ 2.0.1\ x64.tar.bz2
{% endcodeblock %}

If you got the 32-bit installer, just replace the x64 to x32 on the command.

After extracting, you'll get a "Sublime Text 2" folder which contains all files that Sublime Text will need. We have to move that folder to "/opt" folder.
{% codeblock %}
sudo mv Sublime\ Text\ 2 /opt/
{% endcodeblock %}

If you want to be able to run Sublime Text through the terminal by just typing "sublime", we must create a link in "/usr/bin".
{% codeblock %}
sudo ln -s /opt/Sublime\ Text\ 2/sublime_text /usr/bin/sublime
{% endcodeblock %}

Now, we also need to have a launcher in Unity. So we will create a .desktop file in "usr/share/applications".
{% codeblock %}
sudo sublime /usr/share/applications/sublime.desktop
{% endcodeblock %}

This will let Sublime Text 2 open up a blank document named as "sublime.desktop". Paste these line of codes in the document:
{% codeblock %}
[Desktop Entry]
Version=1.0
Name=Sublime Text 2
# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
GenericName=Text Editor

Exec=sublime
Terminal=false
Icon=/opt/Sublime Text 2/Icon/48x48/sublime_text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow

[NewWindow Shortcut Group]
Name=New Window
Exec=sublime -n
TargetEnvironment=Unity
{% endcodeblock %}

There you go! You already have Sublime Text 2 on your machine. If you want to install Sublime Text 3, you can get a `.deb` installer from Sublime Text's [website](http://www.sublimetext.com/3).

###Vim
Other than Subime Text 2, I also use Vim when I develop on Ruby on Rails. Installing Vim is pretty easy, just run `sudo apt-get install vim`

###Git
Git is a version control system used to track the changes of your file/code. It can also be used to collaborate with other developers.

There are two ways of installing Git. It is by installing from source or through `apt-get`. I'll just show the easiest way to install Git, which is using `apt-get`. Just run this command on your terminal to install Git.
{% codeblock %}
sudo apt-get install git
{% endcodeblock %}

If you need a merge tool for Git, I am personally using Meld. You can install it by running:
{% codeblock %}
sudo apt-get install meld
{% endcodeblock %}

###Node.js
{% blockquote Node.js http://nodejs.org/ %}
Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.
{% endblockquote %}

I install node.js is not just for building powerful applications. But also because of <b>NPM (Node Packaged Modules)</b> which is a package manager for Node. I use NPM for installing tools like <b>Grunt</b> and <b>Bower</b> which I also use for developing applications.

I use NVM (Node Version Manager) when installing Node.js because it provides you an easy way to switch between Node.js versions. To install Node.js using NVM, you must first install NVM itself. There two ways of installing NVM. To install NVM using cURL:
{% codeblock %}
curl https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
{% endcodeblock %}

To install NVM using Wget:
{% codeblock %}
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.7.0/install.sh | sh
{% endcodeblock %}

These scripts clones nvm repository to `~/.nvm` and adds the source line to your profile. (`~/.bash_profile` or `~/.profile`)

Once you have installed NVM, you can now use it for installing Node.js. To download, compile and install the latest v0.10.x release of node, do this:
{% codeblock %}
nvm install 0.10  
{% endcodeblock %}

And then you can now use the installed version:
{% codeblock %}
nvm use 0.10
{% endcodeblock %}

###Ruby
I install Ruby because it is required by Octopress which I use for this blog. And not just that, I'm also a Ruby on Rails developer.  We will use RVM for installing Ruby. Before installing Ruby itself, we must first install RVM by running this command.
{% codeblock %}
curl -L https://get.rvm.io | bash -s  stable --ruby
{% endcodeblock %}

After installing RVM, we can now use it to install the latest ruby version.
{% codeblock %}
rvm install 1.9.3
rvm use 1.9.3
rvm rubygems latest
{% endcodeblock %}

###MongoDB
MongoDB is just another database management system that I use for development. MongoDB is actually a relational database. Your data will be stored in a JSON format.

Now, let's install MongoDB  with PHP support.
{% codeblock %}
sudo apt-get install mongodb mongodb-clients php5-dev
{% endcodeblock %}

After installing MongoDB, we must also install the MongoDB-PHP driver. To do that, we must first clone the repository from GitHub
{% codeblock %}
git clone https://github.com/mongodb/mongo-php-driver.git
{% endcodeblock %}

Now, go inside the freshly cloned repo and runt these commands:
{% codeblock %}
cd mongo-php-driver
phpize
./configure
sudo make install
{% endcodeblock %}

Now, we need to copy the driver to php extension directory.
{% codeblock %}
// let's find first the extension directory
php -i | grep extension_dir

// copy the driver to extension directory
sudo cp modules/mongo.so /path/to/php/extesnion_dir/
{% endcodeblock %}

Now, we have to create a mongo.ini file which will be stored in /etc/php5/conf.d/ with the line `extension=mongo.so`.

Finally, restart apache by running `sudo service apache2 restart`

We may also need something like phpMyAdmin for our MongoDB. I use RockMongo. Just download RockMongo from there [website](http://rockmongo.com/downloads) and extract the file to your web server.

###That's it!
I think I've already shared to you all of the important programs and tools that I can't live without :P How about you? What's yours?
