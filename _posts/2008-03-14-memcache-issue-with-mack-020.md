---
layout: post
title: Memcache issue with Mack 0.2.0
tags:
- cachetastic
- General
- mack
- memcache
- News
status: publish
type: post
published: true
meta: {}
---
If you get this error:
<pre>no such file to load -- memcache</pre>
The problem is mack-0.2.0 uses the cachetastic-1.3.1 gem, which has an errant require in the memcache adapter. There will be a patch forthcoming for Mack to use the lastest version of cachetastic which solves this issue.

Until that patch is out, the easiest thing to do is install the memcache-client gem, like such:
<pre>$ sudo gem install memcache-client</pre>
