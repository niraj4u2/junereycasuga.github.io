---
layout: post
title: "Developer Rants: Git commit messages"
date: 2014-05-15 20:31
comments: true
categories: [developer, rant, git, commit, messages, problems]
---

This will be my first post for my Developer Rants series. It will be a series of blog posts of me ranting about some issues or problems I encounter while developing some apps.

<!--more-->

Okay, obviously on this first post, I will be talking about Git commit messages.

### It's not funny
My team is currently developing an app for our company. Being the team lead and head of my department, I always check the commits and pushes of my team on our repository. And I suddenly saw a non-sense commit message. And I'm like, WTF was that!? When I check the changes on that specific commit, it was just a class added on an HTML element. I got really annoyed with what I saw. Some may see this as a funny commit message, but dude, it's a serious business, so it's not funny. Yea, I admit that I'm also doing it before on my personal projects. But for maturity and professionalism's sake, please take commit messages seriously.

### Proper commit message is important
Proper git commit messages are important. Why?

1. It speeds up reviewing process.
2. To help other developers to understand what changes has been made on a specific commit.
3. It is helpful for documenting changes on your project.

{% blockquote Zac Holman %}
Everybody has terrible commit messages in some point in their life.

Sometimes every single day.
{% endblockquote %}

### Making a better Git commit
If you are reading this. And you feel like you're the one I'm referring to, you still have the chance to change this bad habit. 

I am annoyed seeing a 'bug fix' commit messages. It's too broad. And I don't even know what bug was fixed and where it was located.

To make it better, try to limit using `git commit -m "Some crappy commit message here"`. Better to use `git commit` with no flags. By using a simpler git commit command, it will open up Vim (if it's your default editor) where you can construct a better commit message.

Structure your commit message like this:

{% codeblock %}
Short summary of changes (50 chars or less and don't put period at the end)

More detailed description of the changes. This will be good place to
explain what has been changed and why it has been changed. The text
should be wrapped at 72 chars.
{% endcodeblock %}

### Conclusion
Sorry for the rant. It just really annoys me. Anyways, Happy commiting!
