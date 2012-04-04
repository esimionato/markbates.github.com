---
layout: post
title: CoverMe - Code Coverage for Ruby 1.9
tags:
- gem
- News
- rails
- rcov
- release
- Releases
- rspec
- ruby
- testing
- tests
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'yes'
  _edit_last: '1'
  aktt_tweeted: '1'
  _wp_old_slug: ''
---
Ruby 1.9(.2) is an amazing language to develop applications in. It's faster, more powerful, cleaner, and a huge improvement over Ruby 1.8.x. Because of those reasons every Ruby developer should move to this exciting new version of our language.
<div id="_mcePaste">When making a move of this size it's important to have the right tools to help us along. Unfortunately, one of the most useful tools as a Ruby developer, <a href="http://github.com/relevance/rcov">RCov</a>, does not work with Ruby 1.9.</div>
<div id="_mcePaste">RCov, for those unfamiliar analyzes your code and tells you which part of your code was not executed. This is INCREDIBLY useful when hooked up to your test suite. While, it's not the only metric you should use when determining how good your test coverage it, it certainly is a great first step to point out exactly which parts of your code haven't been touched at all!</div>
Enter <a href="http://github.com/markbates/cover_me">CoverMe</a>.
<h2>History</h2>
While working on a Ruby 1.9/Rails 3 project, and loving everything about it (except for the lack of RCov), I came across a <a href="http://engineering.attinteractive.com/2010/08/code-coverage-in-ruby-1-9/">post</a> by Aaron Patterson (of <a href="http://github.com/tenderlove/nokogiri">Nokogiri</a> fame). In this post he quickly outlined a very basic coverage tool using the new built-in Coverage module in Ruby 1.9.

After spending a morning playing with it, I was quickly able to grow the idea into something useful for the project. Later that day the company I was consulting for (<a href="http://www.biddingforgood.com">BiddingForGood.com</a>), and in particular their chief architect, <a href="http://twitter.com/stuartmg">Stuart Garner</a>, told me to take a day or two and clean it up and release it for the world to use, and so <a href="http://github.com/markbates/cover_me">here</a> it is.
<h2>Features</h2>
Here is a brief overview of the features of CoverMe:
<h3>Index Page</h3>
<ul>
	<li>Sortable column headers (File, Lines, Lines of Code, Tested %).</li>
	<li>Searching/filtering by file name.</li>
	<li>Filtering by coverage percent.</li>
	<li>Color coded list of files to quickly see which ones are 100% covered, &gt; 90% covered, or less than 90% covered.</li>
	<li>Large color coded average coverage percent, for quick reference.</li>
</ul>
<h3>Detail Page</h3>
<ul>
	<li>Line by line coverage report</li>
	<li>Color coded lines to quickly see which lines where executed and which ones were not.</li>
	<li>Side by side viewing with the corresponding test/spec file (if one exists).</li>
</ul>
See the <a href="http://github.com/markbates/cover_me">README</a> file for more information on installation and usage.
<h2>Thanks</h2>
I would just quickly like to give another quick thanks to Aaron Patterson for pointing out the Coverage module in Ruby 1.9 and inspiring this, hopefully, helpful little gem. Also another big thanks to Stuart Garner for pushing me to package this up and release it to the world.
<h2>Screenshots</h2>
[gallery link="file"] 
