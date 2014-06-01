---
layout: post
title: "Javascript Event Bubbling and Event Capturing"
date: 2013-03-11 21:10
comments: true
categories: [javascript, bubbling, jquery]
author: Junerey Casuga
---
You might be surprised when you fire an `onClick` event on an element, something happens to another element with the same event. Let's site a clearer example. Suppose  you have an element inside an element with the same event handler which is `onClick`.

<!--more-->

{% img /images/event_bubbling/event_bubbling1.png 350 350 %}

When you click on `element2`, it also cause a click event on `element1`. And that is because of **event bubbling** and **event capturing**.

###Event Bubbling

In event bubbling, the event handler propagates to the outer DOM(Document Object Model).

{% img /images/event_bubbling/event_bubbling.png 350 350 %}

###Event Capturing

In event capturing, the event handler propagates to the inner DOM.

{% img /images/event_bubbling/event_capturing.png 350 350 %}

###How to stop Event  Bubbling?

Event bubbling is always happening when you trigger an event. But there is also a way to stop it. I know that you also don't want event bubbling cause an interference with each element on your DOM. So how can we stop event bubbling? You can stop it by using the `stopPropagation()` method.

{% codeblock lang:javascript %}
$('p').click(function(e){
	e.stopPropagation();
	// do something
});
{% endcodeblock %}

This method allows you to stop the propagation of an event caused by event bubbling. You can also use the `.on()` function of jQuery to stop the propagation of the event.

{% codeblock lang:javascript %}
$('tbody').on('click', 'tr', function(e){
	// do something
});
{% endcodeblock %}

The scripts simply means that by clicking the `tr` element, the propagation stops on the `tbody` element.

That's it for this article. I hope you learned from this. Especially for those who are entering to the front-end development world. Cheers!
