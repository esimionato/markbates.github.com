---
layout: post
title: Configatron 2.0.0 Released!
tags:
- configatron
- General
- News
- Updates
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
I've spent the last few days incorporating Configatron 1.x into the Mack framework, for our forth coming 0.8.0 release. During that time, I've released that Configatron could be better, and that it should be better. I got quickly annoyed with the multiple lines of code I needed to write to just to set a single 'nested' parameter. I got frustrated trying to set default values for libraries, <em>after</em>, I had already loaded the user's configurations. Why couldn't I easily check to see if a parameter was nil or not? So taking all that into account, as well as some great feedback from users, Configatron 2.0.0 was born. It's a complete rewrite of the library. It's quicker, and easier to use.

Just take a look at this example:

<script src="http://gist.github.com/11259.js"></script>

It definitely doesn't get much easier than that!

With this new release you can protect parameters to prevent end users from modifying them:

<script src="http://gist.github.com/11288.js"></script>

Since most configurations systems get loaded before outside libraries, you can run into a problem where the library is expecting certain parameters to be set, but your end user hasn't set them all, they've just set the few that are important to them. So what do you do? You don't want to override the end user's settings, Configatron can now help you with that:

<script src="http://gist.github.com/11289.js"></script>

Of course, these are just some of the enhancements in 2.x Please read the <a href="http://configatron.mackframework.com/" target="_blank">README</a> file and checkout the API for more information.


