---
layout: post
title: My thoughts on spec tests
tags:
- General
- mack
- ruby
- spec test
- testing
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
I've been asked by people why I'm not using spec tests to test Mack. I'm currently using just plain old regular unit tests for my tests. It's a good question, but not really a valid one, I think. Should it matter what type of tests I'm using as long as I'm testing? Tests are tests. The framework you use to do your tests is moot as long as the tests you write are good, solid tests.

I jumped on the spec test bandwagon about a year or so ago. I forced my whole team to start writing in nothing but spec tests. The team, is still not impressed. If I were to tell them we weren't using spec tests anymore, they would be EXTREMELY happy with that.Spec tests are certainly prettier than 'regular' tests. I'll give you that. They are more 'human readable'. With that said I find assert_equal to be fairly easy to read.

So why do I use regular tests, and not spec tests? A couple of reasons. First, they're there and built right in to Ruby, ready to go, no new gems or syntax to learn. They're fast. They are faster than spec tests. I see it everyday at work. I can also, and this one is HUGE, run just a single test or a regex'd series of tests. I really love that last bit. I have yet to find a way to do that, easily, with spec tests.

Again, how people write tests doesn't really matter so much to me, it's just that they write them. Testing is too easy in Ruby, there's just no reason for not writing them.
