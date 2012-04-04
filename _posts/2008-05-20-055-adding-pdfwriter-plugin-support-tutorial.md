---
layout: post
title: ! 'Preview (0.5.5): Adding PDF::Writer Plugin Support Tutorial'
tags:
- engine
- erubis
- gems
- General
- mack
- pdf
- render
- rendering
- Tutorials
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
Ok, let's take the new rendering system out for a spin, shall we? Let's add the PDF::Writer library to our Obligatory Blog Demo application. If you haven't followed this demo you should do that <a href="http://www.mackframework.com/2008/04/18/046-the-obligatory-blog-demo-take-2/" target="_blank">now</a>.

Let's start by requiring the gem in our system. Open up your gems.rb file found in config/initializers and let's add the gem:
<pre>require_gems do |gem|
  gem.add "pdf-writer", :version =&gt; "1.1.8", :libs =&gt; "pdf/writer"
end</pre>
Great! We've told Mack we want to use the 'pdf-writer' gem, version '1.1.8', and we want to automatically require the file 'pdf/writer'. Now, let's install the gem:
<pre>$ sudo rake gems:install</pre>
See how easy this is? We've installed the gem, required the libraries, now we're ready to write our plugin.
<pre>$ rake generate:plugin name=render_pdf</pre>
That should generate a few files/folders in our vendor/plugins directory. Let's open up vendor/plugins/render_pdf/lib/render_pdf.rb and let's start coding.

What we want to do is create a new Mack::Rendering::Engine::Base class so that when we call render(:action) it will have a new engine to render the view file as a PDF.

We'll examine each section in a minute, but for now, let's type this into our render_pdf.rb file:
<pre>module Mack
  module Rendering
    module Engine
      class Pdf &lt; Mack::Rendering::Engine::Base

        def render(io, binding)
          @_pdf = ::PDF::Writer.new
          self.view_template.instance_variable_set("@_pdf", @_pdf)
          eval(io, binding)
          @_pdf.render
        end

        def extension
          :pdfw
        end

        module ViewHelpers
          def pdf
            @_pdf
          end
        end

      end
    end
  end
end
Mack::Rendering::ViewTemplate.send(:include, Mack::Rendering::Engine::Pdf::ViewHelpers)
Mack::Rendering::Engine::Registry.register(:action, :pdf)</pre>
Ok, so on line #4 we extended Mack::Rendering::Engine::Base. This will give us access to a view methods, and will allow us to write to a very simple API. The only method you are <em>absolutely</em> required to implement is the render method. As we can see on line #6, we did just that.

First thing we do in the render method is instantiate a new PDF::Writer class and assign it to an instance variable. We then set that instance variable into the Mack::Rendering::ViewTemplate object we have. We do that because the way the PDF::Writer object works you need to constantly reference the instance of the writer to do your work. Example:
<pre>@_pdf.text "Hello World", :font_size =&gt; 24, :justification =&gt; :center</pre>
On line #9 we eval the io and the binding we've been given. The io will be contents of the view file we have disk, as a String, and the binding will be that of the Mack::Rendering::ViewTemplate object we've been given.

In the extension method we tell the system that are files are going to be found with the extension, pdfw. Another example of this would be the Erubis engine which declares its extension as erb.

The Mack::Rendering::Engine::Pdf::ViewHelpers module we've declared on line #17 is there to hide the @_pdf instance variable with a nicer pdf method. On line #27 we include this module into Mack::Rendering::ViewTemplate so it has access to it.

Finally, and most importantly, we need to register the new engine we've built with the system. We do that on line #28 with this bit of code:
<pre>Mack::Rendering::Engine::Registry.register(:action, :pdf)</pre>
That's saying whenever someone calls render(:action), consider me as an engine to render that. The way the selection of which engine to use is done, is very simple. First come first serve. The engines are in an array, and the first one to have a file with its extension on disk wins. Plain and simple.

Now, let's see all this in action. Let's add PDF support for our 'show' page.

Open up views/posts/show.html.erb and add the following line:
<pre>&lt;%= link_to("pdf", posts_show_url(:id =&gt; @post, :format =&gt; :pdf)) %&gt;</pre>
That will give us a link that looks like '/posts/:id.pdf'. This will, of course, go to our PostsController and the show action. This method does not need to be altered. That's right, you heard me. It does not need to change. Mack will handle the appropriate content-type headers for you. Just another great feature in 0.5.5.

Create a file called views/posts/show.pdf.pdfw. I know this might look a little weird, what with 'pdf.pdfw', but here's the reason why. That's break the file name down into its three parts. 'show' is the name of the action. 'pdf' is the format of the request, think also html, xml, etc... 'pdfw' is the engine we want to use. If we hated ourselves we could do this all in erb with a file called show.pdf.erb, but why would we want to do that?

Anyway, let's dump this nice block of code into our show.pdf.pdfw file:
<pre>pdf.select_font "Times-Roman"
pdf.fill_color(Color::RGB::Red)
pdf.text @post.title, :font_size =&gt; 24, :justification =&gt; :center
pdf.fill_color(Color::RGB::Black)
pdf.text "by #{@post.email}", :font_size =&gt; 12, :justification =&gt; :center
pdf.with_options(:font_size =&gt; 10, :justification =&gt; :left) do |p|
  p.text "\n\n"
  p.text @post.body
  p.text "\n\n"
  p.text "Created at: #{@post.created_at}"
  p.text "Updated at: #{@post.updated_at}"
end</pre>
Since this is not a tutorial on this particular gem, I'm not going to go into what all that does. Instead, let's just have a look at it in action.

Fire up your server:
<pre>$ rake server</pre>
And go to: http://localhost:3000. If you don't already have a post created, create one. Now click on the show link. You should have a link on your page that says 'pdf' click on that link. Voila! You should be seeing a wonderfully formatted PDF right now!

Congrats! You've built a plugin and a new rendering engine for Mack. Now, go crazy!

The source for all this can be found at:Â <a href="http://github.com/markbates/mack_blog_demo/tree/master" target="_blank">http://github.com/markbates/mack_blog_demo/tree/master</a>
