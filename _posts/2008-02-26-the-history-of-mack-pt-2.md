---
layout: post
title: The History Of Mack, pt. 2
tags:
- framework
- General
- mack
- menderchuck
- merb
- mongrel
- rails
- rake
- ramaze
- thin
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
After two years of developing Menderchuck using Rails, I sat down with the VP of Development and the Director of Development and we took at a look at what the future of the company. We reviewed some of the stuff the business would like to build and where the CEO saw the company headed, and we looked at the technologies we were using and determined that it was time to investigate alternatives.

The first things to come under the microscope were Rails/Mongrel. As previously stated we found Rails to be a bit too opinionated for our use. One of the big jokes within the dev team was that I was basically rewriting Rails one section at a time. As sad as that joke is, it's partially true.

I started to investigate other frameworks, particularly Merb and Ramaze, both of which are great frameworks. Both are lightweight and fast, and are a great alternative to Rails. But, they both didn't quite offer what Menderchuck needed to grow into the future.

Menderchuck needed a platform that was fast and scalable. We needed something that would allow us to be a portal application. We needed something that was easy to deploy. We wanted to be able to build/deploy separate applications and have them 'automagically' linked together. And most importantly we needed something very configurable, and less opinionated.

In the search for a framework utopia, I came across two technologies I really fell in love with, <a href="http://rack.rubyforge.org/" target="_blank">Rack</a> and <a href="http://code.macournoyer.com/thin/" target="_blank">Thin</a>.

(More to come...)
