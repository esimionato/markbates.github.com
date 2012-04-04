---
layout: post
title: DataMapper 0.9.x and Mack
tags:
- adam french
- data mapper
- dm-voyeur
- General
- mack
- migrations
- rails conf 08
- sql
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
As I've told a lot of you my goal was to have a Mack release out by the end of RailsConf, which ends tomorrow, that would be rocking the newly released version of DataMapper, 0.9.1. The good news is I've pretty much got it all done, and it works great! The bad news is I'm not going to release it.

Why is this you might ask? Why aren't I going to get Mack support for DataMapper 0.9.1 out there, if it already works. Great questions. The answer is simply this, migrations. I've spent most of the weekend hanging out with a great guy by the name of Adam French. Adam is one of the core developer's of DataMapper. As a matter of fact, I just left Adam after we spent a couple of hours in the hotel bar writing a gem called, dm-voyeur, to allow for 'observing' of DataMapper::Resource objects.

Anyway, as I've been hanging out with Adam I've been trying to upgrade the Mack migration generator script to build the new style format for DataMapper 0.9.1. What I found though, was that migrations have a minor flaw, you have to write the SQL for the column! That means they aren't portable! This bit me in the butt when I had a migration I wrote against Postgres that would run, but wouldn't give me the results I expected in SQLite3. After spending most of the weekend complaining to Adam about this, he kindly pointed out that I have full commit access to DataMapper, and I should probably just fix the bloody thing myself. So that's what I've done.

The great news is that migrations are now pretty sweet. The bad news is I'm not going to release Mack support for DataMapper 0.9.x until they put out the next release so everyone in the Mack universe can have a nice experience using the new migrations. Although I don't know just when the next release of DataMapper will be, I estimate that it will be relatively soon. Keep an eye on this space.
