---
layout: post
title: ! '0.3.0: Adding RSS/xml feeds to our Blog demo'
tags:
- blog
- builder
- demo
- General
- mack
- rss
- ruby
- Tutorials
- xml
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Ok, as you remember a while back we created a simple blog using mack, <a href="http://www.mackframework.com/2008/03/04/the-obligatory-blog-demo/" target="_blank">http://www.mackframework.com/2008/03/04/the-obligatory-blog-demo/</a>. Well now it's time to add the all important RSS/xml feed to it.

Mack 0.3.0 introduces xml rendering support natively, so this shouldn't be so hard. First things first, let's fire up the app, shall we:
<pre>$ rake server</pre>
Now let's head over to http://localhost:3000/posts. We should see our beautiful posts index page. Now let's try to go to http://localhost:3000/posts.xml you should see something that looks like this:

<img src="http://www.mackframework.com/wp-content/uploads/2008/03/xml1.png" alt="XML blog demo 1" width="450" />

Clearly, that's not what we want, is it? I didn't think so. The error is telling us that it's looking for a file called index.xml.erb in the app/views/posts directory of our blog project. Obviously that file doesn't exist.

Let's take a second and talk about <em>why</em> Mack was looking for index.xml.erb. We haven't changed anything in our controller. Our index method still looks something like this:
<pre>def index
  @posts = Post.find(:all)
end</pre>
No where in there does it mention xml. The only place xml is mentioned is on the the url itself, remember? We looked for /posts.xml. By adding .xml you're telling Mack that you want to render, well... xml. So it goes looking for that. That's also new in 0.3.0. The default is html, but if you append a format (.js, .xml, etc...), it will go looking for app/views/&lt;controller_name&gt;/&lt;action_name&gt;.&lt;format&gt;.erb and render it.

Ok, now that we understand why we're looking for an xml file, let's fire up our trusty text editor and create a new file called: app/views/posts/index.xml.erb. Let's edit the file to look like this:
<pre>xml.instruct! :xml, :version=&gt;"1.0"
xml.rss(:version =&gt; "2.0") do
  xml.channel do
    xml.title("My Mack Blog")
    xml.link(posts_index_full_url)
    xml.description("Find out about all the cool stuff happening on my blog!")
    xml.language("en-us")
    xml.copyright("Copyright Me")
    xml.pubDate(CGI.rfc1123_date(Time.now))
    xml.lastBuildDate(CGI.rfc1123_date(Time.now))
    @posts.each do |post|
      xml.entry do
        xml.title(post.title)
        xml.link(posts_show_full_url(:id =&gt; post.id))
        xml.description(post.body)
        xml.pubDate(post.created_at.strftime("%a, %d %b %Y %H:%M:%S"))
      end
    end
  end
end</pre>
Mack uses the standard builder gem library. I'm not going to go into explaining how that works, there are plenty of other tutorials and documentation that will show you that. I'm also not going to explain all the necessary pieces of an RSS feed. Instead I'll point out in that code you'll see we're using the @posts instance variable that we set in the index action of our PostsController. Just like regular *.html.erb files we have access to all the instance variables from the controller, as well, helpers, etc...

So now if we go to http://localhost:3000/posts.xml we should see our RSS feed. If we did a view source we should see something that looks like this:
<pre id="line1"><span class="pi">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span>
&lt;<span class="start-tag">rss</span><span class="attribute-name"> version</span>=<span class="attribute-value">"2.0"</span>&gt;
 &lt;<span class="start-tag">channel</span>&gt;
  &lt;<span class="start-tag">title</span>&gt;My Mack Blog&lt;/<span class="end-tag">title</span>&gt;
  &lt;<span class="start-tag">link</span>&gt;http://localhost:3000/posts&lt;/<span class="end-tag">link</span>&gt;
  &lt;<span class="start-tag">description</span>&gt;Find out about all the cool stuff happening on my blog!&lt;/<span class="end-tag">description</span>&gt;
  &lt;<span class="start-tag">language</span>&gt;en-us&lt;/<span class="end-tag">language</span>&gt;
  &lt;<span class="start-tag">copyright</span>&gt;Copyright Me&lt;/<span class="end-tag">copyright</span>&gt;</pre>
<pre id="line9">  &lt;<span class="start-tag">pubDate</span>&gt;Tue, 18 Mar 2008 17:18:05 GMT&lt;/<span class="end-tag">pubDate</span>&gt;
  &lt;<span class="start-tag">lastBuildDate</span>&gt;Tue, 18 Mar 2008 17:18:05 GMT&lt;/<span class="end-tag">lastBuildDate</span>&gt;
  &lt;<span class="start-tag">entry</span>&gt;
   &lt;<span class="start-tag">title</span>&gt;My New Post&lt;/<span class="end-tag">title</span>&gt;
   &lt;<span class="start-tag">link</span>&gt;http://localhost:3000/posts/1&lt;/<span class="end-tag">link</span>&gt;
   &lt;<span class="start-tag">description</span>&gt;This is my first post in my cool Mack blog!&lt;/<span class="end-tag">description</span>&gt;</pre>
<pre id="line15">   &lt;<span class="start-tag">pubDate</span>&gt;Tue, 18 Mar 2008 11:58:30&lt;/<span class="end-tag">pubDate</span>&gt;
  &lt;/<span class="end-tag">entry</span>&gt;
 &lt;/<span class="end-tag">channel</span>&gt;
&lt;/<span class="end-tag">rss</span>&gt;</pre>
Awesome! All that's really left is create one of those fancy RSS tags in the location field of our browsers that people can click and go straight to the RSS feed. Let's do that now.

At the top of your app/views/posts/index.html.erb file add the following:
<pre>&lt;%= rss_tag(posts_index_url(:format =&gt; :xml)) %&gt;</pre>
Now, refresh the page in your browser, and there you go, you should now see the little RSS button in the location bar of your browser. If you click that you should be taken to your feed.

That's all there is to adding not only xml, but an RSS feed to your new blog.

The code for this demo can be found <a href="http://www.mackframework.com/wp-content/uploads/2008/03/mack_blog_demo.zip" title="Blog Demo w/ XML">here</a>.
