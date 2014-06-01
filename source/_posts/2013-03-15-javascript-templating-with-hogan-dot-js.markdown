---
layout: post
title: "Javascript Templating with Hogan.js"
date: 2013-03-15 23:01
comments: true
categories: [javascript, templating, html, hoganjs]
author: Junerey Casuga
---
Javascript templating is like writing your code in MVC(model-view-controller) pattern which separates the logic from your view. What's good in using templates is it is easy to manage. Imagine your javascript if it looks like this:

<!--more-->

{% codeblock lang:javascript %}
'<div>
	<h2>' + title + '</h2>' + 
	for(var i=0; i < names.length; i++){ +
		'<ul><li>' + names[i] + '</ul>' +
	} +
'</div>'
{% endcodeblock %}

Ugly right? And if you write your javascript in that way, it would be hard for you to maintain it. And for me, it is a bad practice to write your javascript in this way. But if you will use a template, your code will look like this:

{% img /images/templating/template.png %}

Awesome! Much cleaner and it is much easier to maintain. As you can see, it contains HTML tags with some placeholders. And we can replace these with some data which we can also store in a 'json' format:

{% codeblock lang:json %}
{
	"title": "Templating Rocks!",
	"names": {
		"name": "Juan Dela Cruz",
		"name": "Maria Clara"
	}
}
{% endcodeblock %}

And if you combine the template and the data, the result will look like this:

{% codeblock lang:html %}
<h2>Templating Rocks!</h2>
<ul>
	<li>Juan Dela Cruz</li>
	<li>Maria Clara</li>
</ul>
{% endcodeblock %}

To perform javascript templating, you must use a javascript templating engine like Hogan.js which I've used as an example above. Hogan.js is a light-weight templating engine which only has 2.5k file size. It is developed at Twitter and it uses the Mustach templating syntax. Hogan compiles your templates into javascript before use. Which means that it performs faster.

There are more javascript templating engine you can use. But personally, I use Hogan.js because it's minimal and it does not have a lot of features which I would not normally use.

For more information about Hogan.js, just refer to <http://twitter.github.com/hogan.js/>
