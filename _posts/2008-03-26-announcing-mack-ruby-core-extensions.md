---
layout: post
title: Announcing Mack Ruby Core Extensions
tags:
- extensions
- gem
- git
- inflection
- mack
- News
- Releases
- ruby
status: publish
type: post
published: true
meta: {}
---
Mack has been using a combination of the ruby_extensions gem as well some local extensions to the Ruby core in order to make Mack as wonderful as it is. In an effort to make life a little simpler, as well as to help share the wealth, the ruby_extensions gem and the Mack extensions have been combined into a single new gem called mack_ruby_core_extensions.

One of the main Mack pieces that has been broken out into this new gem is the inflection system. Now you can have inflections as part of any Ruby application just by requiring the gem. As far as I can tell this is the first stand alone inflection system for Ruby. I know because I couldn't find one for Mack, that's why I had to write one.

This gem will continually be updated, outside of the core Mack code. The forthcoming release of Mack, 0.4.0, will be converted to use the new gem.

Those who wish to contribute to the gem can find it on GitHub at: <a href="http://github.com/markbates/mack_ruby_core_extensions" target="_blank">http://github.com/markbates/mack_ruby_core_extensions</a>

The API for mack_ruby_core_extensions can be found at:
<a href="http://mrce-api.mackframework.com/" target="_blank">http://mrce-api.mackframework.com/</a>
<pre>Â $ sudo gem install mack_ruby_core_extensions</pre>
