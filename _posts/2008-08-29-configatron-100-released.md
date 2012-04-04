---
layout: post
title: Configatron 1.0.0 Released!
tags:
- configatron
- General
- News
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Configatron makes configuring your applications and scripts incredibly easy. No longer is a there a need to use constants or global variables. Now you can use a simple and painless system to configure your life. And, because it's all Ruby, you can do any crazy thing you would like to! <a href="http://configatron.mackframework.com/">API</a>

<em>Note: Configatron is a general purpose library, that can be used in ANY Ruby application or script, it's not Mack specific. So go on and configure to your hearts content. :)</em>
<pre>$ sudo gem install configatron</pre>
<h2>Examples</h2>
<h3>Simple</h3>
<script src="http://gist.github.com/7986.js"></script>

Now, anywhere in your code you can do the following:

<script src="http://gist.github.com/7987.js"></script>

Viola! Simple as can be.

Now you're saying, what if I want to have a 'default' set of options, but then override them later, based on other information? Simple again. Let's use our above example. We've configured our 'database_url' option to be "postgres://localhost/mack_framework_rocks". The problem with that is that is our production database url, not our development url. Fair enough, all you have to do is redeclare it:

<script src="http://gist.github.com/7988.js"></script>

becomes:

<script src="http://gist.github.com/7989.js"></script>

Notice how our other configuration parameters haven't changed? Cool, eh?
<h3>Namespaces</h3>
The question that should be on your lips is what I need to have namespaced configuration parameters. It's easy! Configatron allows you to create namespaces.

<script src="http://gist.github.com/7990.js"></script>

becomes:

<script src="http://gist.github.com/7992.js"></script>

Configatron allows you to nest namespaces to your hearts content! Just keep going, it's that easy.

Enjoy!
