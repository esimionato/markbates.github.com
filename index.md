---
layout: default
---
{% include JB/setup %}

{% assign post = site.posts.first %} 

<div class="page-header">
  <h1><a href="{{ post.url }}">{{ post.title }}</a></h1>
</div>
{{ post.content }} 