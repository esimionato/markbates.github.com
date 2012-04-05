---
layout: post
title: "Now Blogging with Jekyll"
description: ""
category: 
tags: []
---
{% include JB/setup %}

As you may or may not have noticed there's a new blog in town! That's right, I've ditched the zero, WordPress, and got with the hero, <a href="https://github.com/mojombo/jekyll" target="_blank">Jekyll</a>. And I have to say, it sure feels good.

WordPress worked well for me for years, but I have to say that I never enjoyed the process of writing a technical blog in a browser. I hated the lack of tools that my editor has at it's disposal. It was too slow to do previews with. And all together it just always felt a bit "hacky", and not in a good way.

Jekyll let's me write my blog entries in my favorite local text editor. I can preview my blog, locally, which is great if you want to make a sweeping change to the whole thing. When I'm done writing I can do a <code>git push</code> and my site now has all the new content.

{% highlight ruby %}
class Foo < ActiveRecord::Base

  def do_something
    %w{a b c}.each do |x|
      puts "#{x}"
    end
  end

end
{% endhighlight %}
sadfasfasfdsf
{% highlight JavaScript %}
  foo = function() {
    
  }
{% endhighlight %}