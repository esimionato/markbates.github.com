---
layout: post
title: Configatron 1.1.0 Released
tags:
- configatron
- General
- News
- Updates
- yaml
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
On the heels of last week's successful <a href="http://www.mackframework.com/2008/08/29/configatron-100-released/">release</a> of Configatron 1.0.0 comes version 1.1.0. The big addition, feature wise, to 1.1.0 is the ability to now load configurations from a YAML file.
<pre>configatron.configure_from_yaml('/path/to/file.yml')</pre>
When reload is called on configatron any YAML files will be read back in from disk, allowing you to change your configurations and reload them.

Enjoy!
