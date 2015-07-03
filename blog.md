---
title: BLOG
layout: post_index
---

{% for post in paginator.posts %}
<div class="row-fluid">
  <div class="span12">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <h4>{{ post.date | date_to_long_string }}</h4>
    {{ post.excerpt }}
      <p><a href="{{ post.url }}">Read the whole Post</a>
    </p>
  </div>
</div>
{% endfor %}
