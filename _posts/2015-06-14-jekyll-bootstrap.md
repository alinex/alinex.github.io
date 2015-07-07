---
title: Jekyll & Bootstrap on Github
layout: post
tags: Jekyll Bootstrap Git Github
---

I red about the Jekyll support on github and had to try it mysqlf. I already
have a small site on github but was not aware of the whole functionality which
was behind it.

So I read a lot more about Jekyll and the newest version of Bootstrap to make a
new and modern website representing my web development. My hope was to get something
a web developer can easily maintain and use while working in the development
environment and with the all to familiar tools.


## About

#### Jekyll

[Jekyll](http://jekyllrb.com/) is a ruby software which transforms plain text
into static web pages and blogs. It recreates the site any time the sources
changed and run a webserver for delivery.

#### Bootstrap

[Bootstrap](http://getbootstrap.com/) is a popular client framework to create
mobile friendly websites. It was first build at Twitter.

#### Github Pages

The [github pages](https://pages.github.com/) allows the developer to create a free of charge
website on github. It is used the same way as you create your code. Make a
repository, commit your changes and push it to the master. A few minutes later
the website is up to date.


## First Steps

I already had a github page so i use this repository as base for the new site. If
you don't have such you make create it first.

To test my Jekyll site locally before pushing it I wanted a local installation.
So I first installed it locally and started therefore with the ruby installation:

{% highlight bash %}
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -L https://get.rvm.io | bash -s stable --ruby
source /home/alex/.rvm/scripts/rvm
{% endhighlight %}

I had to install it this way because the package manager contains a too old version
1.9 which won't work.

I added the `Gemfile` with the following content to my repository:

{% highlight text %}
source 'https://rubygems.org'
gem 'github-pages'
{% endhighlight %}

Now I installed Jekyll through the bundler:

{% highlight bash %}
gem install bundler
bundle install
{% endhighlight %}

## Start local Jekyll

The following call within the repository will start the Jekyll server:

{% highlight bash %}
source /home/alex/.rvm/scripts/rvm
bundle exec jekyll serve
{% endhighlight %}

And with the additional flag `--drafts` the posts of the _drafts folder are shown
as if they are already released.

It will also continually detect file changes and recreates the pages so you can
change the files and directly view the changes.

## Upload to github

Like working with git code you add your files, commit the changes and push it to
master - that's all.

## Optimize Jekyll

Within the optimization I did the following and edited the `_config.yml`:

``` yaml
highlighter: pygments
markdown: redcarpet
timezone: Europe/Berlin

title: Alinex

paginate:    5
paginate_path: "blog/page:num"
```

That will enable code highlighting for code marked with triple backticks like done
on markdown. And enable the pagination to be used on the blog index.

### Blog Index

TO generate a blog in which I will put some posts each week I generated the following
`blog/index.html`:

``` mustache
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


{% if paginator.total_pages != 1 %}
<div class="row-fluid text-center text-caps">
  <div class="span12">
  <hr />
  <nav class="pagination" role="pagination">

<span class="page-number">Page {{ paginator.page }} of {{ paginator.total_pages }}</span>
{% if site.paginate_path != 'page:num'%}
{% assign paginate_url = site.paginate_path | remove:'/page:num' %}
{% if paginator.previous_page %}
  {% if paginator.previous_page == 1 %}
  <a class="newer-posts" href="{{ site.url }}/{{ paginate_url }}/" class="btn" title="Newer Posts">&larr; Newer Posts</a> &nbsp; &nbsp;
  {% else %}
 <a class="newer-posts" href="{{ site.url }}/{{ paginate_url }}/page{{ paginator.previous_page }}/" class="btn" title="Newer Posts">&larr; Newer Posts</a>
  {% endif %}
{% endif %}
{% if paginator.next_page %}
&nbsp; &nbsp; <a class="older-posts" href="{{ site.url }}/{{ paginate_url }}/page{{ paginator.next_page }}/" class="btn" title="Older Posts">Older Posts &rarr;</a>
{% endif %}
{% else %}
{% if paginator.previous_page %}
  {% if paginator.previous_page == 1 %}
  <a class="newer-posts" href="{{ site.url }}/" class="btn" title="Newer Posts">&larr; Newer Posts</a> &nbsp; &nbsp;
  {% else %}
 <a class="newer-posts" href="{{ site.url }}/page{{ paginator.previous_page }}/" class="btn" title="Newer Posts">&larr; Newer Posts</a>
  {% endif %}
{% endif %}
{% if paginator.next_page %}
&nbsp; &nbsp; <a class="older-posts" href="{{ site.url }}/page{{ paginator.next_page }}/" class="btn" title="Older Posts">Older Posts &rarr;</a>
            </nav>
{% endif %}
{% endif %}
  </div>
</div>
{% endif %}
```

The first block prints one page of posts and the second (more complex) block
will create links to page through all of the posts.

### Tags

And as I will add tags to each post I will create a lookup per tag on the sidebar
which is realized with the following `_includes/tags.html`:

``` mustache
<div class="posts">
  <h4>Show Posts by Tag</h4>

  <!-- collect tags -->
  {% capture tags %}
    {% for tag in site.tags %}
      {{ tag[0] }}
    {% endfor %}
  {% endcapture %}
  {% assign sortedtags = tags | split:' ' | sort %}

  <script>
  switchTag = function (tag) {
    val = document.getElementById('tag4'+tag).style.display == 'block' ? 'none' : 'block';
    document.getElementById('tag4'+tag).style.display = val;
  }
  </script>

  <p>
    {% for tag in sortedtags %}
      <a onclick="switchTag('{{ tag }}')">{{ tag }}</a>
    {% endfor %}
  </p>

  {% for tag in sortedtags %}
    <div id="tag4{{ tag }}" style="display:none">
    <h4 onclick="switchTag('{{ tag }}')">Posts about: {{ tag }}</h4>
    {% for post in site.tags[tag] %}
      <p><a href="{{ post.url }}">{{ post.title }}</a></p>
    {% endfor %}
    </div>
  {% endfor %}

  <p><br /><br /><br /></p>

</div>
```

THis will collect all tags out of the posts add a function for show/hide the
links per tag and list the tag links in separate blocks.

## Bootstrap

To get a modern design with less effort which will also have a mobile representation
I choose bootstrap with it's sow/column design to do the work.

I am new to bootstrap but had the layout ready after 2 hours of testing and
optimizing.

After some more tests I got ít even better and could bring my layout to be
display size independent as responsive site. Some areas will show one under each
other on small displays while others will be hidden.

Also an optimized print-layout is given by hiding all navigation blocks.

And finally I got the correct colors and style with a simple and small css file
which mostly set fonts, colors and tweak spaces a little.

## Final thoughts

After a short test weekend I got solution looking good and functional. I will
continue to use it and I can also say that it is a good solution for the programmer
and makes maintaining the developer's site as easy as maintaining the code.

Sorry for the very abstractive and short explanation, but more detailed ones will
follow in the future.

<p class="text-right"><i>Alex</i></p>