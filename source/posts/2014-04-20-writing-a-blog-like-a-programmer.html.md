---
title: Writing a blog like a programmer
date: 2014-04-20
disqus: af605546-db91-4eda-aca6-b53cb1b285f5
published: true
---

When I wanted to write a blog I had only a few requirments

* to use markdown
* to show pretty code segments in my blog posts
* to have a comment system

READMORE
It turns out, it is not so easy to find a blogging platform
with these capabilities, or maybe I just didn't put a lot of
effort in finding a good one.

# Wordpress is not for me

My first attempt was to use Wordpress, and I could only say that it
was a horrible experience for me. In wordpress I had too much of
everything, and all the things I would never use took up all the
space.

The editor is plain and doesn't support markdown
so writing code segments is much harder than it needs to be.
If I want to customize something I would have to use
php, and wordpress made look php far worse than it really
is. Really, php isn't such a bad language, but wordpress flavored php
makes me want to stop being a developer.

Of course, I understand that WordPress isn't aimed for people who
know how to code, but for normal everyday people wanting to write
articles without worrying about anything. For them it is fine I guess,
but for me it was horrible.

# Svbtle, Medium and Ghost lack features

While I like all three of them, especially svbtle, they all lack
something that makes my blogging life more painful than it should be.
For example svbtle lacks a commenting system, and while I could
imagine that you can communicate with your readers in some other way
I still think that comments could help a lot. Disqus for example
is just great.

The other thing that these platforms lack is the ease of customization.
One thing I often want to change are the colors in the code section. The
other thing is font size, because I really enjoy large readable fonts
that can be read even if you are not sitting really close to your screen.

# Thats why I decided to roll my own blogging system

This was the last option I have considered because blogs are now days
so common that writing your own feels like reinventing the wheel.
But still I have done it, and it is just great. From the start I was
pretty much sure I don't need a database, or some complicated web server.
A markdown compiler and a static file hosting will do just fine.

For a markdown generator I used Middleman, and for the hosting Github
pages. I have also written several scripts that will generate me a new
post file, deployment scripts, and some to run and manage local testing
and publishing. Also I had to come up with a proper design, to choose a
font, and to implement the css and layout files on my own.

The overall setup took me around a week, but I only worked on it after
work in the evening. A week of development is too much in comparison
to an out of the box platform like wordpress, but the benefits I got are
amazing. _Finally I can enjoy blogging the way I always wanted_.

In some future post I will probably write about the technical details
behind the blog. Now I only want to brag a little, and express my
positive feeling towards Github pages and Middleman.
