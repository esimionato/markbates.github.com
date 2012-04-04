---
layout: post
title: Horrible bug in DataMapper 0.3.0
tags:
- bug
- class
- comparable
- data mapper
- General
- tests
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
<a href="http://wm.lighthouseapp.com/projects/4819-datamapper/tickets/185-including-comparable-in-class-class-breaks-test-unit-and-probably-more#ticket-185-8" target="_blank">http://wm.lighthouseapp.com/projects/4819-datamapper/tickets/185-including-comparable-in-class-class-breaks-test-unit-and-probably-more#ticket-185-8</a>

In the gem at the bottom of lib/data_mapper/support/typed_set.rb there is the following code:
<pre>class Class
Â Â include Comparable
Â Â def &lt;=&gt;(other)
Â Â  Â name &lt;=&gt; other.name
Â Â end
end</pre>
This causese Test::Runner to through up an error similar to this:
<pre>/usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:25:in `collect': undefined method `suite' for Gem::LoadError:Class (NoMethodError)
from /usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:23:in `each_object'
from /usr/local/lib/ruby/1.8/test/unit/collector/objectspace.rb:23:in `collect'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:58
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:213:in `[]'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:213:in `run'
from /usr/local/lib/ruby/1.8/test/unit/autorunner.rb:12:in `run'
from /usr/local/lib/ruby/1.8/test/unit.rb:278
from /usr/local/lib/ruby/gems/1.8/gems/rake-0.8.1/lib/rake/rake_test_loader.rb:5
rake aborted!</pre>
It also causes your tests to blow up and not run. Which, if you're trying to do any development causes some real problems! If you comment out 'include Comparable' from Class things seem to work just fine. I say seem, because I haven't done any real extensive testing with this. The other thing you can do is revert to 0.2.5, but that's up to you. Either way, it's not really optimal. Let's hope they fix this soon.
