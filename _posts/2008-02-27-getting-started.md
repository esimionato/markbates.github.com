---
layout: post
title: Getting Started
tags:
- gem
- mack
- Tutorials
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Installing Mack is pretty simple:
<pre>$ sudo gem install mack</pre>
This will install a few gems that Mack is dependent on. Once you've got all the gems installed you can create your mack app with the following:
<pre>$ mack my_cool_mack_app</pre>
That should create a folder called my_cool_mack_app with a bunch of files and folders underneath it. Now, to fire up the app:
<pre>$ cd my_cool_mack_app
$ rake server</pre>
Now point your browser to http://localhost:3000 and you should see a nice "welcome to mack" screen.

That's it. Now you can start rocking your super cool application.
