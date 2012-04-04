---
layout: post
title: (0.6.0) 4 Little Known Mack Features
tags:
- exceptions
- General
- mack
- redirects
- rendering
- routes
status: publish
type: post
published: true
meta:
  _edit_last: '1'
  _wp_old_slug: 5-little-known-mack-features
---
I thought it might be fun to start posting about some of the little known features in Mack. There are a treasure trove of them in there, so let's pick a couple and start there.
<h3>render(:url)</h3>
This is a great little feature, one of my personal favorites. In your views you can do things like this:
<pre>&lt;%= render(:url, "http://www.mackframework.com) %&gt;</pre>
that will render the contents of http://www.mackframework.com into your view. You can also do 'local' urls.
<pre>&lt;%= render(:url, "/users/1") %&gt;</pre>
will make an internal request to your application and render the results of "/users/1" into your view.Â The optional 3rd parameter to render allows you to do things like set the HTTP method:
<pre>&lt;%= render(:url, "/users/1", :method =&gt; :post) %&gt;</pre>
or add parameters you want to pass to the URL you want to render:Â 
<pre>&lt;%= render(:url, "/users/1", :method =&gt; :post,Â :parameters =&gt; {:id =&gt; 1}) %&gt;</pre>
<h3>Error handling in routes</h3>
Routing allows you to define controllers/actions you want to catch and handle exceptions that happen in other controllers. Let's look at the following routes.rb file:
<pre>Mack::Routes.build do |r|
  r.resource :users
  r.home_page "/", :controller =&gt; :default, :action =&gt; :index
  r.handle_errors ArgumentError, :controller =&gt; :problems, :action =&gt; :arguments
  r.handle_errors DataMapper::ObjectNotFoundError, :controller =&gt; :problems, :action =&gt; :not_found
  r.defaults
end</pre>
What's going on with r.handle_errors you ask? Well, first we tell the routing system which error we want to capture in our controllers, DataMapper::ObjectNotFoundError, then we tell it which controller and which action we want to handle that error.

When an exception is thrown during a request Mack checks to see if that exception has been registered, if it has been then the request gets forwarded to the defined controller and action for handling. So in the above example if a DataMapper::ObjectNotFoundError is raised, the request will be forwarded to the ProblemsController, not_found action.

One of the really nice things about this is that you have access to the original request, so you can't get the page the person was trying to access, any parameters that were passed, etc... You also have access the exception itself with theÂ caught_exception method.
<h3>Server-side redirects</h3>
Let's be honest, redirects are the most exciting topic, and this is the first of two sections on it! I'll try to be brief. When dealing with redirects it can sometimes be helpful to do a server-side redirect. The difference, for those who don't know, between a server-side redirect and a regular redirect is the following. With a regular redirect the response is sent back down to the client's browser, which then issues another response back to the server for the new url that was specified in the previous response. You'll often hear this referred to as a client-side redirect. A server-side redirect sends you to a different url on the server, without first sending down a response to the client. Because of this the client only gets one response.

To do a server-side redirect in Mack is very easy. Here's what a client side redirect in an action would look like:
<pre>redirect_to(users_index_url)</pre>
To make that a server-side redirect you would simply pass an extra option to the redirect_to method:
<pre>redirect_to(users_index_url,Â :server_side =&gt; true)</pre>
<h3>Redirects in routes</h3>
This is a cool little feature. Let's say that you have changed a few urls around. You want a quick way to redirect people who have bookmarked the old urls to the new urls. You could have a controller that did nothing but that, but that seems like a lot of extra work, and it's really something that your routing system should be doing for you anyway. Enter redirects in routes.
<pre>Mack::Routes.build do |r|
Â Â r.old_foo "/my_old_foo", :redirect_to =&gt; "/my_new_foo", :status =&gt; 301
end</pre>
From now on anything comes in to "/my_old_foo" will be redirected to "/my_new_foo" with a status of 301.
