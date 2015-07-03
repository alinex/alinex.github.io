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

It will also continually detect file changes and recreates the pages so you can
change the files and directly view the changes.

## Upload to github

Like working with git code you add your files, commit the changes and push it to
master - that's all.

## Bootstrap

To get a modern design with less effort which will also have a mobile representation
I choose bootstrap with it's sow/column design to do the work.

I am new to bootstrap but had the layout ready after 2 hours of testing and
optimizing.

## Final thoughts

After a short test weekend I got solution looking good and functional. I will
continue to use it and I can also say that it is a good solution for the programmer
and makes maintaining the developer's site as easy as maintaining the code.

Sorry for the very abstractive and short explanation, but more detailed ones will
follow in the future.

<p class="text-right"><i>Alex</i></p>