---
layout: post
title: Let's talk DataMapper
tags:
- active record
- benchmark
- data mapper
- General
- mack
- orm
- tests
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
As you may, or may not know, DataMapper is the new ORM framework on the scene these days in the Ruby world. It's getting a lot of hype for being clean, fast, simple, and feature rich. Oh, and it's not ActiveRecord. I think that seems to be the real thing that is driving people to DataMapper, the fact that it's not ActiveRecord.

I will say DataMapper is clean, simple, and feature rich. In 0.3.0 they've added migrations, which is great. Btw, a little off topic, but I'm working on migration support for both ActiveRecord and DataMapper in Mack as we speak. It should, hopefully, be out sometime this week. What I won't give DataMapper is that it's fast. In my tests, and I'll provide some number below, DataMapper only seems to win on inserts, after that ActiveRecord beats it hands down. In all fairness to DataMapper I'm starting to think that the problems are not at the DataMapper layer, but at the underlying Data Objects layer that DataMapper uses. As you'll see from my tests DataMapper seems very heavilyÂ optimizedÂ towards MySQL over PostgreSQL. This, to me, leans towards a difference in the underlying adapters.

Another problem I have with DataMapper is that I have to set the 'properties' of the model inside the model itself. It's an old school approach, and it does have the benefit of being self documenting, but it also has the drawbacks of constantÂ maintenanceÂ and clutter at the top of your model. Not to mention potential conflicts when running through migrations, etc...

I'm also having one other little problem these days. This has only been a problem since I've gone DataMapper 0.3.0. At the end of some of rake tasks, if I have DataMapper required, I get this:

Â 
<pre>/usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:25:in `collect': undefined method `suite' for Gem::VerificationError:Class (NoMethodError)
from /usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:23:in `each_object'
from /usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:23:in `collect'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:58
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:213:in `[]'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:213:in `run'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:12:in `run'
from /usr/local/lib/ruby/1.8/test/unit.rb:278</pre>
The rake task completed successfully, but I get this fairly random error message. If anyone out there is also getting this message, please let me know what it is. I'm open for ideas on this one.

Despite these issues I have with DataMapper, I'm going to keep striving to provide support for both it and ActiveRecord in Mack. I think it's important to give people a choice and not force them to use the one I think is either easier to code for, or better. Both of which I'm not saying about ActiveRecord, but in technologies in general.

Anyway, enough of my blather, here are the test results I was speaking about:

Â 

<span style="color: #800000;">Running time 1.693881 seconds. [MESSAGE]: DM: postgresql: Inserts</span>
Running time 2.799189 seconds. [MESSAGE]: AR: postgresql: Inserts

Running time 1.368185 seconds. [MESSAGE]: DM: postgresql: Individual Reads
<span style="color: #800000;">Running time 0.734143 seconds. [MESSAGE]: AR: postgresql: Individual Reads</span>

Running time 0.917551 seconds. [MESSAGE]: DM: postgresql: Bulk Reads
<span style="color: #800000;">Running time 0.121198 seconds. [MESSAGE]: AR: postgresql: Bulk Reads</span>

Running time 2.309244 seconds. [MESSAGE]: DM: postgresql: Updates
<span style="color: #800000;">Running time 2.079578 seconds. [MESSAGE]: AR: postgresql: Updates</span>

Running time 1.802914 seconds. [MESSAGE]: DM: postgresql: Deletes
<span style="color: #800000;">Running time 1.708714 seconds. [MESSAGE]: AR: postgresql: Deletes</span>

<span style="color: #800000;">Running time 0.433761 seconds. [MESSAGE]: DM: mysql: Inserts</span>
Running time 2.621093 seconds. [MESSAGE]: AR: mysql: Inserts

Running time 1.073741 seconds. [MESSAGE]: DM: mysql: Individual Reads
<span style="color: #800000;">Running time 0.207305 seconds. [MESSAGE]: AR: mysql: Individual Reads</span>

Running time 0.827842 seconds. [MESSAGE]: DM: mysql: Bulk Reads
<span style="color: #800000;">Running time 0.073593 seconds. [MESSAGE]: AR: mysql: Bulk Reads</span>

<span style="color: #800000;">Running time 1.204845 seconds. [MESSAGE]: DM: mysql: Updates</span>
Running time 1.738602 seconds. [MESSAGE]: AR: mysql: Updates

<span style="color: #800000;">Running time 1.010774 seconds. [MESSAGE]: DM: mysql: Deletes</span>
Running time 1.251691 seconds. [MESSAGE]: AR: mysql: Deletes

Â 

Â 
