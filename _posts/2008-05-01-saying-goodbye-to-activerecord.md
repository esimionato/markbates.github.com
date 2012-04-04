---
layout: post
title: Saying Goodbye to ActiveRecord
tags:
- active record
- data mapper
- General
- mack
- News
- orm
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
I've been wrestling with this for a while now, and I've finally made my peace with it. I've decided to remove native support for ActiveRecord from Mack. From now on it'll be DataMapper by default, out of the box. This was not an easy decision to make. Essentially it boils down to one of the key tenants of Mack, use the best of breed technologies to build a best of breed framework. I truly feel that DataMapper, especially when it hits the 0.9.0 release, is the best ORM, and persistence, system out there. I also feel that it is a natural fit for the Mack framework.

The other reason why I made the decision was time. It's very time consuming to constantly maintain two different, and with 0.9.0 extremely different, ORMs. There are plenty of features that I could've done faster, had I only been supporting the one ORM.

Now I know I might come under fire from some people for this, but it's a decision that I think is best for the framework. If some enterprising developer out there wants to build a plugin, or a gem, that adds ActiveRecord support, then I'm all for it! Please do!

The question you're probably asking yourself now, is when will this be happening. It'll be happening in the next release of Mack, probably the end of this week or the beginning of next week.

Again, I'm sorry for those of you were hoping to use ActiveRecord with Mack. Check out DataMapper, I'm sure you'll be happy with it.

Comments?
