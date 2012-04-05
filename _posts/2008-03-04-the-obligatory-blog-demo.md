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

{% highlight ruby %}
class Post < DataMapper::Base
  property :title, :string
  property :email, :string
  property :body, :text
  property :created_at, :datetime
  property :updated_at, :datetime

  validates_presence_of :title
  validates_presence_of :body
  validates_presence_of :email
end
{% endhighlight %}

Now, I'm not going to go into detail as to what that's doing, that's for the guys at DataMapper to explain. Before we move on to the next step, you'll probably want to crack open config/database.yml and edit it so it the paths to your database are correct, you'll probably also want to go to your database system and make sure that the database name you configured in your config/database.yml is created, otherwise this will be a very short trip. I'll wait while you do that. Finished, great! Let's move on.

We need to now open a Mack console so we can create the tables needed for our blog.
<pre>$ rake console
$ Post.table.create!
$ exit</pre>
Ok, we should now have a posts table in our new database. Isn't life wonderful? We're so close to showing the world how wonderful we are as developers.

Now let's edit our views, so they look something like this:

app/views/posts/index.html.erb:
{% highlight erb %}
<h1>Listing posts</h1>

<table>
  <tr>
    <th>Title</th>
    <th>Body</th>
    <th>Email</th>
  </tr>

<% for post in @posts %>
  <tr>
    <td><%=post.title %></td>
    <td><%=post.body %></td>
    <td><%=post.email %></td>
    <td><%= link_to("Show", posts_show_url(:id => post.id)) %></td>
    <td><%= link_to("Edit", posts_edit_url(:id => post.id)) %></td>
    <td><%= link_to("Delete", posts_delete_url(:id => post.id), :method => :delete, :confirm => "Are you sure?") %></td>
  </tr>
<% end %>
</table>

<br />

<%= link_to("New Post", posts_new_url) %>
{% endhighlight %}
app/views/posts/edit.html.erb:
<pre><h1>Edit post</h1>

<%= error_messages_for :post %>

<form action="<%= posts_update_url(:id => @post.id) %>" class="edit_post" id="edit_post" method="post">
  <input type="hidden" name="_method" value="put">
  <p>
    <b>Title</b><br />
    <input id="post_title" name="post[title]" size="30" type="text" value="<%= @post.title %>" />
  </p>

  <p>
    <b>Body</b><br />
    <textarea id="post_body" name="post[body]"><%= @post.body %></textarea>
  </p>

  <p>
    <b>Email</b><br />
    <input id="post_email" name="post[email]" size="30" type="text" value="<%= @post.email %>" />
  </p>

  <p>
    <input id="post_submit" name="commit" type="submit" value="Create" />
  </p>
</form>

<%= link_to("Back", posts_index_url) %></pre>
app/views/posts/show.html.erb:
<pre><p>
  <b>Title:</b>
  <%= @post.title %>
</p>

<p>
  <b>Body:</b>
  <%= @post.body %>
</p>

<p>
  <b>Email:</b>
  <%= @post.email %>
</p>

<p>
  <b>Created at:</b>
  <%= @post.created_at %>
</p>

<p>
  <b>Updated at:</b>
  <%= @post.updated_at %>
</p>

<%= link_to("Edit", posts_edit_url(:id => @post.id)) %> |
<%= link_to("Back", posts_index_url) %></pre>
app/views/posts/new.html.erb:
<pre><h1>New post</h1>

<%= error_messages_for :post %>

<form action="<%= posts_create_url %>" class="new_post" id="new_post" method="post">
  <p>
    <b>Title</b><br />
    <input id="post_title" name="post[title]" size="30" type="text" value="<%= @post.title %>" />
  </p>

  <p>
    <b>Body</b><br />
    <textarea id="post_body" name="post[body]"><%= @post.body %></textarea>
  </p>

  <p>
    <b>Email</b><br />
    <input id="post_email" name="post[email]" size="30" type="text" value="<%= @post.email %>" />
  </p>

  <p>
    <input id="post_submit" name="commit" type="submit" value="Create" />
  </p>
</form>

<%= link_to("Back", posts_index_url) %></pre>
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
<pre>r.home_page "/", :controller => :default, :action => :index</pre>
so that it's now:
<pre>r.home_page "/", :controller => :posts, :action => :index</pre>
Now all you have to do is to restart your server and Bob's your uncle when you hit http://localhost:3000 again you should your fantastic posts index page.

This concludes our brief introductory tutorial on getting going on Mack. Obviously Mack does a lot more, and I highly encourage you to read the <a href="http://api.mackframework.com">RDoc</a> to find out more about what it can do.

Enjoy.
