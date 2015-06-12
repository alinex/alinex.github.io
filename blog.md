---
title: BLOG
layout: default
---

# {{ page.title }}

{% for post in site.posts limit: 5 %}
<div class="row-fluid">
  <div class="span12">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <h4>{{ post.date | date_to_long_string }}</h4>
    {{ post.content | truncatewords: 60 }}
      <p><a href="{{ post.url }}">Read the whole Post</a>
    </p>
  </div>
</div>
{% endfor %}
