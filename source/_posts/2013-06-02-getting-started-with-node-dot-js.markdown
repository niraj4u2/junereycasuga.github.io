---
layout: post
title: "Getting started with Node.js"
date: 2013-06-02 14:22
comments: true
categories: [node, javascript, backend]
author: Junerey Casuga
---
You may have heard about Node.js but you don't know what exactly it does. To make it short and simple, Node.js allows you to run Javascript code in the backend. 

<!--more-->

###Installing Node
Before we start on writing an app, we need to install it first in our machine. For MacOS and Windows, there's a pretty straight forward installers which you can find on [nodejs.org](http://nodejs.org). For Linux, you can run these lines of command on your terminal:

{% codeblock %}
sudo apt-get install python-software-properties python g++ make
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
{% endcodeblock %}

###Hello World
We have node on our machine now. So let's proceed on writing our first node.js app, our ever loving "Hello World".

Fire up your favorite text editor and create a file called <i>helloworld.js</i>. Now, we want node to write "Hello World". So put these code on <i>helloworld.js</i>:

{% codeblock lang:javascript %}
console.log("Hello World");
{% endcodeblock %}

Save it and execute it using Node.js by running this command on your terminal:

{% codeblock %}
node helloworld.js
{% endcodeblock %}

This should print "Hello World" on your terminal.

###Write everything
Unlike PHP, you have Apache that can receive HTTP requests and serve web pages. With node, you also have to implement your own HTTP server.

It may sound difficult, but it's not. Thanks to the modules that came with Node itself. I will show how to write your own HTTP server later.

###Modules
Node.js has module to make your life (somewhat) easier. Modules are encapsulated piece of codes. Means that a module contains functions related to the subject of the module. Let's just take the 'http' module as an example. This module, obviously, contains functions specific to HTTP. So how do we use these modules? Just use the require function.

{% codeblock lang:javascript %}
var http = require('http');
{% endcodeblock  %}

Other than the module that came along with Node, you can also write your own module and you can include it to your app by:

{% codeblock lang:javascript %}
var http = require('./yourModule.js');
{% endcodeblock %}

You can also install new modules with the help of Node Package Manager(NPM) which came along with Node.js as you install it. To install new modules using NPM, fire up your terminal, navigate to your app directory, and run this command:

{% codeblock %}
npm install module_name
{% endcodeblock %}

###Writing your HTTP Server
As I promised, we will write our own HTTP server using Node.js. Create a new JS file named <i>server.js</i> and put this codes inside the file.

{% codeblock lang:javascript %}
var http = require("http");

http.createServer(function(request,response){
	response.writeHead(200, {"Content-type":"tex/plain"});
	response.write("Hello World");
	response.end();
}).listen(8888);
{% endcodeblock %}

Now, run this command using your terminal:

{% codeblock %}
node server.js
{% endcodeblock %}

Fire up your browser and navigate to `http://localhost:888`. Your browser should be able to run a page displaying the text "Hello World".

Sweet! So let me explain what we have written.

The first line requires the <i>http</i> module that comes with Node.js and makes it accessible throught the <i>http</i> variable.

Then we called one of <i>http</i> module's function which is the createServer function. This function returns an object and this object has a method <i>listen</i>. The <i>listen</i> method accepts a numeric value which indicates the port number the HTTP server is going to listen on.

And inside the function we used the <i>response.writeHead()</i> function to send a HTTP status code(200, means success) and a content-type in the  HTTP response header. The <i>response.write()</i> function sends the "Hello World" text to the HTTP response body. And the <i>write.end()</i> ends the response. 

###Routing
Now, we also need to handle URL, GET, and POST parameters into our router. We may need to include the <i>url</i> and <i>querystring</i> to able to do this. 

The <i>url</i> module allows us to extract different parts of a URL.

The <i>querystring</i> module parses the body of a GET or POST requests.

But we will concentrate on using the <i>url</i> module for now.

{% codeblock lang:javascript %}
var http=require("http"),
	url=require("url");

http.createServer(function(request, response){
	var pathname = url.parse(request.url).pathname;
	console.log("Request for " + pathname + " received.");

	response.writeHead(200, {"Content-type":"text/plain"});
	response.write("Hello World");
	response.end();
}).listen(8888);
{% endcodeblock %}

Save it, and run {% codeblock %}node server.js{% endcodeblock %}. Open up your browser and navigate to `http://localhost:8888`.

As you run it through the browser, you should be able to see the requested url on your command line.

So, we just included the <i>url</i> module and made it accessible through the <i>url</i> variable. Then we parsed the request and passed it to <i>pathname</i> variable. 

###Conclusion
That's it for now. I'm also new to Node.js and this is just what I've learned over the weekend. I just want to share it to you. Node.js requires extra effort but creating a powerful app with Node.js is worth it.

This is just a preview of what you should know about Node.js. If you want to make your life easier, you might want to pick a framework for Node.js like [Express](http://expressjs.com/) and [Partial](http://www.partialjs.com/).
