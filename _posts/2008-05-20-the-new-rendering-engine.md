---
layout: post
title: ! 'Preview (0.5.5): The New Rendering Engine'
tags:
- erb
- erubis
- General
- haml
- mack
- markaby
- rendering
status: publish
type: post
published: true
meta:
  _edit_last: '1'
---
In the latest version of Mack the rendering engine has been completely re-written from the ground up. With this comes some new features, some incompatibility, and most importantly,Â extensibility. Let's jump on in and see what we can expect with this release.
<h3>Incompatibility</h3>
<ul>
	<li>Gone is &lt;%= @content_for_layout %&gt; in layouts. In is &lt;%= yield_to :view %&gt;.</li>
	<li>Gone is render(options_hash) in controllers/views. In is render(type, value, options_hash)
Examples:
render(:action =&gt; :new) is now render(:action, :new)
render(:url =&gt; "http://www.mackframework.com", :parameters =&gt; {:message =&gt; "hi"}) is nowÂ render(:url, "http://www.mackframework.com", :parameters =&gt; {:message =&gt; "hi"})</li>
	<li>Gone is *.xml.erb. In is *.xml.builder</li>
</ul>
<div>Let's quickly talk about how theseÂ incompatibilitiesÂ have come about. First there were several bugs that needed to be addressed with the rendering engine. For example, if you set an instance variable in a view, it wasn't available in the layout. That's a pain if you want to do things like programatically set the page title. There were also 'hacks' used to do things like render xml using the Builder::XmlMarkup library. It wasn't clean, but it worked. Finally, the rendering engine itself wasn't that extensible. All of that has now changed.</div>
<div></div>
<h3>Render Me Softly</h3>
In the new rendering engine there are two parts to the system, Mack::Rendering::Type::* objects and Mack::Rendering::Engine::* objects. Let me explain the difference.
<h4>Mack::Rendering::Type::*</h4>
A type is something like :action, :text, :inline, :url, etc... That is the type of thing you want to do. I want to render an action. I want to render a url, etc... There are classes for each of these types, and you can easily add your own. These types do all sorts of work before they pass it off to an engine, if need be. For example, in the case of Mack::Rendering::Type::Partial the render method does the work of inserting an '_' in the appropriate place, so the file can found.
<pre>&lt;%= render(:partial, "users/form") %&gt; # =&gt; "users/_form"</pre>
Once that happens it tries to find an engine to process the partial.
<h4>Mack::Rendering::Engine::*</h4>
An engine does the actual work of rendering the io, with the binding of the Mack::Rendering::ViewTemplate object, it's been given by the results of the render method in the Mack::Rendering::Type::* object. Engine examples would be, Erubis (ERB), Markaby, Haml, and Builder::XmlMarkup, all of which are included with Mack in this release. New engines can easily be plugged in and registered with the system.

Coming soon a tutorial on adding PDF::Writer support using the new system.
