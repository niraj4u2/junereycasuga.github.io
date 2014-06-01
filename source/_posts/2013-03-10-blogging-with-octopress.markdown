---
layout: post
title: "Blogging with Octopress"
date: 2013-03-10 14:01
comments: true
categories: [octopress, jekyll, blog]
author: Junerey Casuga
---
Octopress is actually a framework for Jekyll. But before I continue, let me first tell you what Jekyll is. Jekyll is knwon as "a simple, blog aware, static site generator". But Jekyll is not a blogging software. It is a parsing engine. It means that Jekyll parses your dynamic components such as templates, partials, markdown/textiles, etc. into a static site. 

<!--more-->

Moving on. I started blogging using Wordpress and I found it too much for "not really a blogger" people like me. It is too much for me. And I don't want to be writing inside a big database. That's why I've decided to write my blog using Jekyll since it is light-weight and you can write your post using your favorite text editor. But I had a hard time using because you need to build everything for your blog site. You have to write your own HTML template, CSS, JavaScripts and set up your own configurations.

Then the time came that I've encountered Octopress. As I've said, it is a framework for Jekyll. In Octopress, you don't have to write your own HTML templates, CSS and JavaScripts becuase Octopress already have them all for you. I'll walk you through how to start blogging using Octopress.

Before you start using Octopress, you must first install these:

1. Git
2. Ruby 1.9.3

###Setting up Octopress

First of all you must clone Octopress from GitHub. Just run this command.

{% codeblock %}
git clone git://github.com/imathis/octopress.git octopress
{% endcodeblock %}

Next is to install the dependencies.

{% codeblock %}
cd octopress
gem install bundler
bundle install
{% endcodeblock %}

Installing the default Octopress theme.

{% codeblock %}
rake install
{% endcodeblock %}

After performing these steps, you can configure your blog by editing some files. Here are the list of files for configuring Octopress:

{% codeblock %}
_config.yml    # Main config
Rakefile       # Config for deployment
config.rb      # Compass config
config.ru      # Rack config
{% endcodeblock %}

To create a new post, just run this on your terminal:

{% codeblock %}
rake new_post["title"]
{% endcodeblock %}

By running this command, Rake(Ruby Make) will generate a markdown file that will be saved in the `source/_posts` and you can use that file for writing your article.

For more documentations about posting new article and creating a new page, please refer to Octopress documentation at <http://octopress.org/docs/blogging/>.

There you go! I hope I was able to help you to set up your blog using Octopress. Enjoy blogging!

###Resources:
<http://jekyllbootstrap.com/lessons/jekyll-introduction.html>

<http://octopress.org/>
