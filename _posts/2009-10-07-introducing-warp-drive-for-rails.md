---
layout: post
title: Introducing Warp Drive for Rails
tags:
- engines
- gem
- General
- News
- rails
- release
- Releases
- warp drive
status: publish
type: post
published: true
meta:
  aktt_notify_twitter: 'yes'
  _edit_last: '1'
  aktt_tweeted: '1'
---
At work recently we had a need to build a large Rails application that we then wanted to, for lack of a better word, subclass. Unfortunately there is no real good way of doing that. Rails Engines and templates have way too may limitations. We wanted to bundle up the entire Rails app (models, controllers, views, routes, migrations, configurations, libs, assets, etc... everything!), but there was no good way of doing that. Well, now there is, it's called the Warp Drive.

I've decided to just include my README file below to explain what it is, since it's a bit lengthy, and I don't feel like retyping.

This is still in it's early stages, so use with care, but it does seem to be working for us on a daily basis. Let me know what you think!
<h2>What is Warp Drive?</h2>
Warp Drive is what Rails Engines wish they could be, and more! They kick Rails templates in the ass, and they beat keeping an ever evolving base Rails app up to date.
<h3>What are Rails Engines?</h3>
Rails Engines allow you to package up some of a Rails app (controllers, models, views, routes, libs) and put them in a plugin that can be included into a new Rails app, thereby giving it the functionality you had in the engine. That sounds good, but what about the downsides of using an engine? Well, you can't override or extend any of the functionality from the engine in your main application. You can hack at the plugin, but now you've made it difficult to update. So what do you do if you want to add or alter a method to a controller or model? What do you do if you want to change the look and feel of a view? You have to copy everything into your main application. Boo!

Rails Engines also don't allow you to package up migrations, assets, plugins, initializers, etc... All the fun stuff that you've come to know and love about a Rails application.
<h3>Enter the Warp Drive!</h3>
So what is a Warp Drive? Great question. To put it simply a Warp Drive is a standard, full featured, Rails application that you can easily bundle up into a Ruby Gem, and include into another Rails app. That second Rails app now has all the power of the first Rails. That is all there is to it.
<h2>Creating a Warp Drive.</h2>
Let's assume we have an application that implements AuthLogic for handling user registration/authentication. We have controllers, views, models, plugins, initializers, configurations, migrations, tasks, etc... it's a full featured fully functional Rails application, we call it authenticator.

We want to turn our authenticator application into a Warp Drive. We can do it in three simple steps, the first two steps you only need to do the first time, to set everything up.
<ol>
	<li><code>$ gem install warp_drive</code></li>
	<li><code>$ warpify</code>
That will add a little bit of code to your <code>Rakefile</code>. That code simply requires the Warp Drive gem, and gives you hooks to configure the gem of your Warp Drive application.</li>
	<li>$ <code>rake warp_drive:compile</code> (<code>rake warp_drive:install</code>)This will either compile your gem for your (<code>warp_drive:compile</code>) or compile and install your gem (<code>warp_drive:install</code>)</li>
</ol>
That's it! You should now have your Rails application bundled up and/or installed as a RubyGem!
<h2>Using a Warp Drive.</h2>
With your fancy new Warp Drive, authenticator, built and installed how do you use it in that new application your building? Again, it's stupid easy, and it only takes one step, that only needs to be run once:
<ol> <code>$ install_warp_drive authenticator</code></ol>
That will put a few lines of code in your <code>Rakefile</code>, so you have access to all the <code>Rakefile</code> tasks in your Warp Drive, and a line in your <code>config/environment.rb</code> so that it will load your Warp Drive when you launch your application.

That's it! You're done. Now you can run <code>rake db:migrate</code> to run the migrations from both your Warp Drive and your new application. Enjoy!
<h2>Overriding, Extending, and Other Such Fun Things</h2>
<h3>Overriding and Extending</h3>
You've been enjoying your new Warp Drive back application for a little while now, but you decide you really need to change an action in your controller, how do you go about that? Simple, just like you would any normal alteration to a Ruby class.

Example:
Here is what the action looks like in our Warp Drive UsersController:
<pre><code>
  def new
    @user = User.new
  end
</code></pre>
In our new application we can just open up the UsersController like this:
<pre><code>
  class UsersController &lt; ApplicationController

    def new_with_default_name
      new_without_default_name
      @user.login = 'default_name'
    end

    alias_method_chain :new, :default_name

  end
</code></pre>
Viola! The same works for any thing else in the system, models, libs, etc... In our example we used <code>alias_method_chain</code> to retain the original method, but we could have completely rewritten the method as well.

You can also plop in a new view and it will override the view that was in your Warp Drive. The sky is really the limit.
<h3>Assets</h3>
You can easily bundle assets from your public directory in your Warp Drive. Just make sure they are in folders called <code>warp_drive</code>. Those folders will then be symlinked to your new project's public directory when the application starts up.
<h3>Keep Those Rake Tasks Private!</h3>
We all them, Rake tasks we have created to help us do all sorts of things, and we usually don't want them to ship. Well, Warp Drive has you covered there. Just place your tasks in folders called <code>private</code> and Bob's your uncle they won't be available in the compiled gem.
<pre><code>
  lib/
    tasks/
      foo.rake
      private/
        bar.rake
</code></pre>
In this example <code>foo.rake</code> will be available to clients of your Warp Drive, but <code>bar.rake</code> will not be.

Copyright (c) 2009 Mark Bates
