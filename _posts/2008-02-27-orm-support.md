---
layout: post
title: ORM Support
tags:
- active record
- data mapper
- orm
- Tutorials
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
If you would like to add ORM support to your application, it's simple. Out of the box Mack has support for two popular ORMs, ActiveRecord and DataMapper.Our tests show that DataMapper is 10x slower then ActiveRecord, but who knows, your mileage my vary.

When you create your mack app you can do the following which will add ORM support to your generated app:
<pre>$ mack my_cool_mack_app -o activerecord</pre>
If you already have a mack app you can very easily add ORM support by adding the following configuration parameter to the default.yml file:
<pre>mack::orm: activerecord</pre>
And also add a database.yml file to your config directory that looks like this:
<pre>development:
  adapter: mysql
  database: my_cool_mack_app_development
  host: localhost
  username: root
  password:

test:
  adapter: mysql
  database: my_cool_mack_app_test
  host: localhost
  username: root
  password:

production:
  adapter: mysql
  database: my_cool_mack_app_production
  host: localhost
  username: root
  password:</pre>
