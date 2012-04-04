---
layout: post
title: ! '''Helpers'' in Mack'
tags:
- application helper
- General
- helpers
- mack
- modules
- rails
- rdoc
- Tutorials
status: publish
type: post
published: true
meta: {}
---
Let's talk a bit about 'helpers' in Mack, shall we?
<h2>How does Rails handle helpers?</h2>
Those ofÂ  you familiar with Rails are already familiar with this concepts. In Rails helpers are modules of code that get included into views for certain controllers, or all controllers in the case of ApplicationHelper. These helpers are meant to clean up the views and encapsulate commonly used Ruby code and keep it out of the views. In Rails 2.0 it's easier now to include some of these helper methods into the controller, but by default, they're not readily available.
<h2>How does Mack handle helpers?</h2>
Mack deals with helpers a little differently. Let's start with ApplicationHelper. In Rails, ApplicationHelper gets included into all the views for every controller. This is extremely useful, and from my experience it's the most used helper in Rails. The same is true of Mack. Regardless of which controller/view you're in, ApplicationHelper is there to assist. This brings us to our first difference between Rails and Mack:

<strong>* ApplicationHelper is included into both the views AND the controllers.</strong>

That's right, you no longer have to do special voodoo magic to get the contents of ApplicationHelper included into your controller, it's right there by default, ready to go. Now, I know at this stage you're saying, if ApplicationHelper is included into all controllers, as well as views, then aren't the methods in there publicly accessible as actions? The answer is no. Which brings us to our next point on helpers:

<strong>* All helper public helper methods are converted to protected methods prior to be included into controllers/views.</strong>

By converting all public methods in helpers to protected methods we get around the security concerns regarding the methods becoming publicly available actions in the controllers.

Now, in Rails when you create a controller it creates a new helper module file for that controller. The idea being that you can put helpers into this module that are only available to that controller's views.

<strong>* Mack helpers are NOT controller specific.</strong>

Mack, doesn't do what Rails does in this respect. It's been my personal experience that these files end up empty and just take up space on my disk. So screw em! We don't need em.
<h2>Mack only helper concepts</h2>
Ok, so we've covered the basics of helpers, let's talk about a couple of concepts that are available only in the Mack world.
<h3>Controller Helpers:</h3>
What are controller helpers? In my experience working with Rails I found that I would have 'helper' methods, protected or private of course, in my controllers that were meant to assist the actual actions in that controller. Two things eventually dawned on me. The first was that I'm cluttering up my controllers with all these helper methods. The second was that there should be a way to share these amongst other controllers that could probably use them as well. (Example, methods dealing with authentication)

In the Rails world I wrote a gem, controller_helpers, that helps to facilitate this. Well, being as this is the Mack world, this facility is built right in.

If you go and create a module in the app/helpers folder that's follows the naming convention &lt;controller_name&gt;Helper then it will automatically be included into the appropriate controller. Two things to note here, the security model is still applied, public methods become protected methods. The second is these methods are available in that controller ONLY. They are not available in other controllers or any views within that controller.
<pre>class BlogController &lt; Mack::Controller::Base
  before_filter :authenticate
end</pre>
<pre>module BlogControllerHelper
  def authenticate
    # do work to authenticate user here...
  end
end</pre>
As we see the controller name in the previous example was BlogController and it's helper name was BlogControllerHelper. Now in the example we had an authenticate method in BlogControllerHelper, we realize that we also want to use that in our CommentsController as well. So we can refactor that example to look like this:
<pre>class BlogController &lt; Mack::Controller::Base
  before_filter :authenticate
end

class CommentsController &lt; Mack::Controller::Base
  before_filter :authenticate
end</pre>
<pre>module AuthenticationControllerHelper
  def authenticate
    # do work to authenticate user here...
  end
  include_safely_into(BlogController, CommentsController)
end</pre>
Here you can see in our new AuthenticationControllerHelper module we use the include_safely_into method. This method is documented in the RDoc for Mack, but basically what it does is includes that module into the list of Classes defined, and changes it's public methods to protected.

Now we have included controller helpers into several different controllers. This helps to keep our controllers limited to just actions, and helps us to reuse code in other places. All very good things.
<h3>Refactoring ApplicationHelper</h3>
So, if you're like me, your Rails ApplicationHelper module is absolutely overflowing with all sorts of bits of code. In one project I have it's 682 lines of code! Some code does authentication like stuff, is_logged_in?, is_logged_out?, etc... some does formatting, some does other stuff. It's a big steaming pile of unrelated code.

In Mack you can solve this problem by breaking your code out into Mack::ViewHelpers::&lt;module_name&gt; modules. IfÂ  you do this then that module is automatically included into all views. Modules in the Mack::ViewHelpers namespace do NOT get included into the controllers. If you want to include them into controllers you can use the include_safely_into method to achieve that goal.
<h2>Conclusion</h2>
Well, I hope you enjoyed, and are still awake, this brief overview of the way helpers work in Mack. They are different from Rails. I feel these differences are what make Mack helpers really really useful. Mack helpers do more then Rails, and these features can be not only be really powerful, but can really help to keep your code nice and DRY.

Enjoy.
