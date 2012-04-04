---
layout: post
title: Using Sprockets without Rails
tags:
- book
- coffee script
- coffeescript
- General
- rack
- rails
- ruby
- sprockets
- Tutorials
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'yes'
  _edit_last: '1'
  aktt_tweeted: '1'
---
I've started working this week on an example application for the next book I'm about to write and I wanted a simple way for my readers to easily run the app (it's going to be a single HTML file with a ton of cool JavaScript going on in it). My first choice for running this app was to use the popular Ruby library, <a href="http://rack.rubyforge.org/" target="_blank">Rack</a>. If you are unfamiliar with Rack, please check it out. It provides a simple interface for writing web applications. By writing a simple Ruby file readers can use their favorite Rack compatible web server to launch the application. Sounds simple, eh? That's because it is.

With a simple Rack application written in a few lines of code I was able to start developing my example application. That's when I realized I needed a good way to serve up all my <a href="http://jashkenas.github.com/coffee-script/" target="_blank">CoffeeScript</a> and <a href="http://sass-lang.com/" target="_blank">Sass</a> files. I was going to write a watchr script that did this, but I thought that was a bit heavy handed, and not very flexible, so I turned to <a href="https://github.com/sstephenson/sprockets" target="_blank">Sprockets</a>.

Sprockets recently gained a lot of attention because it is bundled in with <a href="http://guides.rubyonrails.org/3_1_release_notes.html" target="_blank">Rails 3.1</a> to serve up an application's assets. It's a clever little library that will process your files using CoffeeScript, Sass, etc... and let you bundle them up in to a single asset by using a manifest. That was exactly what I wanted. After I spent the better part of an afternoon doing a bit of research and debugging here is the Rack configuration file I came up with:

<script src="https://gist.github.com/1184400.js"> </script>

That will serve
<pre>/assets/application.css</pre>
via Sprockets. The file itself will live in
<pre>&lt;pwd&gt;/app/assets/stylesheets/application.scss</pre>
The same goes for JavaScript files.

Hopefully this will save someone else a little of time when they're trying to do the same thing. Enjoy!
