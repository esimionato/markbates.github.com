---
layout: post
title: ! '0.1.0: The Obligatory ''Blog'' Demo'
tags:
- blog
- data mapper
- demo
- mack
- post
- scaffold
- tutorial
- Tutorials
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Ok, because every good framework should tell you how to create a blog, why should Mack be any different? Let's start off with the basics. Is Mack installed? If not, here's how:
<pre>$ sudo gem install mack</pre>
Great! Before we move on, make sure that the gem you installed is at LEAST version 0.1.0, otherwise, you're not going to get very far in this tutorial. Now, let's move on. Now let's generate our kick ass new blog, and since we're going to need some sort of database support for our blog, we'll configure it to use DataMapper. If you don't have DataMapper installed, please head over to <a href="http://datamapper.org" target="_blank">http://datamapper.org</a> to find out how to install it. Mack has support for ActiveRecord as well, but it's just easier to get DataMapper going because you don't have to deal with migrations.
<pre>$ mack my_kick_ass_blog -o data_mapper
$ cd my_kick_ass_blog</pre>
That should've created a whole bunch of files and folders for your blog. Now let's generate some scaffold code for our blog:
<pre>$ rake generate:scaffold name=posts</pre>
That should've created even more files for you. One of those files is app/models/post.rb, let's open that up, so we can edit it for DataMapper.

Edit the file so it looks something like this:
<pre>class Post &lt; DataMapper::Base
  property :title, :string
  property :email, :string
  property :body, :text
  property :created_at, :datetime
  property :updated_at, :datetime

  validates_presence_of :title
  validates_presence_of :body
  validates_presence_of :email
end</pre>
Now, I'm not going to go into detail as to what that's doing, that's for the guys at DataMapper to explain. Before we move on to the next step, you'll probably want to crack open config/database.yml and edit it so it the paths to your database are correct, you'll probably also want to go to your database system and make sure that the database name you configured in your config/database.yml is created, otherwise this will be a very short trip. I'll wait while you do that. Finished, great! Let's move on.

We need to now open a Mack console so we can create the tables needed for our blog.
<pre>$ rake console
$ Post.table.create!
$ exit</pre>
Ok, we should now have a posts table in our new database. Isn't life wonderful? We're so close to showing the world how wonderful we are as developers.

Now let's edit our views, so they look something like this:

app/views/posts/index.html.erb:
<pre>&lt;h1&gt;Listing posts&lt;/h1&gt;

&lt;table&gt;
  &lt;tr&gt;
    &lt;th&gt;Title&lt;/th&gt;
    &lt;th&gt;Body&lt;/th&gt;
    &lt;th&gt;Email&lt;/th&gt;
  &lt;/tr&gt;

&lt;% for post in @posts %&gt;
  &lt;tr&gt;
    &lt;td&gt;&lt;%=post.title %&gt;&lt;/td&gt;
    &lt;td&gt;&lt;%=post.body %&gt;&lt;/td&gt;
    &lt;td&gt;&lt;%=post.email %&gt;&lt;/td&gt;
    &lt;td&gt;&lt;%= link_to("Show", posts_show_url(:id =&gt; post.id)) %&gt;&lt;/td&gt;
    &lt;td&gt;&lt;%= link_to("Edit", posts_edit_url(:id =&gt; post.id)) %&gt;&lt;/td&gt;
    &lt;td&gt;&lt;%= link_to("Delete", posts_delete_url(:id =&gt; post.id), :method =&gt; :delete, :confirm =&gt; "Are you sure?") %&gt;&lt;/td&gt;
  &lt;/tr&gt;
&lt;% end %&gt;
&lt;/table&gt;

&lt;br /&gt;

&lt;%= link_to("New Post", posts_new_url) %&gt;</pre>
app/views/posts/edit.html.erb:
<pre>&lt;h1&gt;Edit post&lt;/h1&gt;

&lt;%= error_messages_for :post %&gt;

&lt;form action="&lt;%= posts_update_url(:id =&gt; @post.id) %&gt;" class="edit_post" id="edit_post" method="post"&gt;
  &lt;input type="hidden" name="_method" value="put"&gt;
  &lt;p&gt;
    &lt;b&gt;Title&lt;/b&gt;&lt;br /&gt;
    &lt;input id="post_title" name="post[title]" size="30" type="text" value="&lt;%= @post.title %&gt;" /&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;b&gt;Body&lt;/b&gt;&lt;br /&gt;
    &lt;textarea id="post_body" name="post[body]"&gt;&lt;%= @post.body %&gt;&lt;/textarea&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;b&gt;Email&lt;/b&gt;&lt;br /&gt;
    &lt;input id="post_email" name="post[email]" size="30" type="text" value="&lt;%= @post.email %&gt;" /&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;input id="post_submit" name="commit" type="submit" value="Create" /&gt;
  &lt;/p&gt;
&lt;/form&gt;

&lt;%= link_to("Back", posts_index_url) %&gt;</pre>
app/views/posts/show.html.erb:
<pre>&lt;p&gt;
  &lt;b&gt;Title:&lt;/b&gt;
  &lt;%= @post.title %&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;b&gt;Body:&lt;/b&gt;
  &lt;%= @post.body %&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;b&gt;Email:&lt;/b&gt;
  &lt;%= @post.email %&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;b&gt;Created at:&lt;/b&gt;
  &lt;%= @post.created_at %&gt;
&lt;/p&gt;

&lt;p&gt;
  &lt;b&gt;Updated at:&lt;/b&gt;
  &lt;%= @post.updated_at %&gt;
&lt;/p&gt;

&lt;%= link_to("Edit", posts_edit_url(:id =&gt; @post.id)) %&gt; |
&lt;%= link_to("Back", posts_index_url) %&gt;</pre>
app/views/posts/new.html.erb:
<pre>&lt;h1&gt;New post&lt;/h1&gt;

&lt;%= error_messages_for :post %&gt;

&lt;form action="&lt;%= posts_create_url %&gt;" class="new_post" id="new_post" method="post"&gt;
  &lt;p&gt;
    &lt;b&gt;Title&lt;/b&gt;&lt;br /&gt;
    &lt;input id="post_title" name="post[title]" size="30" type="text" value="&lt;%= @post.title %&gt;" /&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;b&gt;Body&lt;/b&gt;&lt;br /&gt;
    &lt;textarea id="post_body" name="post[body]"&gt;&lt;%= @post.body %&gt;&lt;/textarea&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;b&gt;Email&lt;/b&gt;&lt;br /&gt;
    &lt;input id="post_email" name="post[email]" size="30" type="text" value="&lt;%= @post.email %&gt;" /&gt;
  &lt;/p&gt;

  &lt;p&gt;
    &lt;input id="post_submit" name="commit" type="submit" value="Create" /&gt;
  &lt;/p&gt;
&lt;/form&gt;

&lt;%= link_to("Back", posts_index_url) %&gt;</pre>
Ok, so now we've created our forms, and setup our index page. Let's actually go to the site and see it all works!

First we need to start the server:

$ rake server

Now let's head on over to http://localhost:3000/posts and see what we've got. You should see a page that looks something like this:

<img src="http://www.mackframework.com/wp-content/uploads/2008/03/12.png" alt="Blog Demo 1" />

Now let's click on that 'New Post' link and fill out the form:

<img src="http://www.mackframework.com/wp-content/uploads/2008/03/21.png" alt="Blog Demo 2" />

Now, let's hit that wonderful 'Create' button and see what happens!

<img src="http://www.mackframework.com/wp-content/uploads/2008/03/31.png" alt="Blog Demo 3" />

Congrats! You just created your first blog post! Now let's head back to http://localhost:3000/posts and see what we've got.

<img src="http://www.mackframework.com/wp-content/uploads/2008/03/41.png" alt="Blog Demo 4" />

Wonderful! Now all that's left to do is to set our home page to our posts index page. Let's open up our config/routes.rb and edit the following line:
<pre>r.home_page "/", :controller =&gt; :default, :action =&gt; :index</pre>
so that it's now:
<pre>r.home_page "/", :controller =&gt; :posts, :action =&gt; :index</pre>
Now all you have to do is to restart your server and Bob's your uncle when you hit http://localhost:3000 again you should your fantastic posts index page.

This concludes our brief introductory tutorial on getting going on Mack. Obviously Mack does a lot more, and I highly encourage you to read the <a href="http://api.mackframework.com">RDoc</a> to find out more about what it can do.

Enjoy.
