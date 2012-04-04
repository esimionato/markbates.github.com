---
layout: post
title: ORMs and Mack
tags:
- active record
- data mapper
- General
- github.com
- mack
- News
- rake
- sequel
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
So a lot has been made in the last few days about my decision to drop ActiveRecord's native support in <a href="http://www.mackframework.com/2008/05/01/saying-goodbye-to-activerecord/" target="_blank">Mack</a>. People have asked why can't I keep what I already have in regards to support for ActiveRecord, and why can't I support Sequel. So, I've decided to compromise.

In the next version of Mack, which should be out in the next day or two, I've broken out support for ActiveRecord and DataMapper into their own gems,Â <a href="http://github.com/markbates/mack-orm/tree/master" target="_blank">http://github.com/markbates/mack-orm/tree/master</a>. That means you'll be able to still use ActiveRecord, if you want. The default ORM, however, will be DataMapper. That's what you'll get out of the box with Mack.

Now, keeping with my original post, I'll be actively maintaining the mack-data_mapper gem, and when I can I'll make similar changes to the mack-active_record, but I'm not promising anything. Now the good thing here is that since the repos for these gems are on GitHub, anyone can contribute changes/additions to them. I've even put a stub in there for Sequel support, that's definitely something someone else will have to support.

This also has a nice advantage in keeping the Mack core clean and simple. Hopefully this will all lead to faster development time turn around for Mack.

It's also worth noting that when I talk about 'native' support, all I mean is some Rake tasks and some generators. There's nothing stopping anyone from using ANY ORM with Mack. You could even create your own, if you really wanted to.

Here's to hoping this makes everyone happy!
