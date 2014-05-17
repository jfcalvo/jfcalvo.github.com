---
type: post
layout: default
title: Some useful Ruby/Rails Gems
summary: A list of interesting and useful Ruby and Rails Gems.
language: english
---

From time to time I find some really interesting Ruby/Rails Gems that make our daily work as developers easier. In this article I will talk about some of those Gems.

## Ruby Gems

### [lunchy][lunchy]

Control MacOS services using `launchctl` is a pain so `lunchy` offer us a really easy wrapper around `launchctl` command.

To show all the available services in your system you can use the command `lunchy ls:

{% highlight bash %}
$ lunchy ls
com.spotify.webhelper
com.valvesoftware.steamclean
homebrew.mxcl.elasticsearch
homebrew.mxcl.memcached
homebrew.mxcl.postgresql
homebrew.mxcl.redis
org.virtualbox.vboxwebsrv
{% endhighlight %}

To start/stop `memcached` you can use `start` and `stop` commands:

{% highlight bash %}
$ lunchy stop memcached
stopped homebrew.mxcl.memcached
$ lunchy start memcached
started homebrew.mxcl.memcached
{% endhighlight %}

Installation:

{% highlight bash %}
$ gem install lunchy
{% endhighlight %}

### [ruby-progressbar][ruby-progressbar]

This gem allow us to use a nice progressbar in our shell scripts to show information to the user on how the progression of the script is.

{% highlight bash %}
Progress: |===================================                 |
{% endhighlight %}

Very useful when you have an script that take a lot of time and you want to know how many time remains to finish. The gem has a lot of parameters to customize the progressbar including estimated time of arrival (ETA).

Installation:

{% highlight bash %}
$ gem install ruby-progressbar
{% endhighlight %}

### [sanitize][sanitize]

Sanitize is a gem that allow us to clean dirty and not valid HTML in a very easy way. If you have some HTML string content and you want for example to export it to a XML field sanitize will help you to clean those HTML strings into valid ones.

The fast way to clean a HTML string is using the `clean` method that will use the default parameters:

{% highlight ruby %}
sanitize.clean(my_html_string)
{% endhighlight %}

Installation:

{% highlight bash %}
$ gem install sanitize
{% endhighlight %}


## Rails Gems

### [dotenv-rails][dotenv-rails]

This useful gem allow Rails applications to automatically load `.env.development` into environment `ENV` when Rails is in development mode, `.env.test` when you are in test mode and `.env` when the app is executing in production.

I think that this gem is so useful that this should be integrated by default on Rails itself.

Installation:

Add the following line to you `Gemfile`.

{% highlight ruby %}
gem 'dotenv-rails', :groups => [:development, :test]
{% endhighlight %}

[lunchy]: https://github.com/mperham/lunchy
[ruby-progressbar]: https://github.com/jfelchner/ruby-progressbar
[sanitize]: https://github.com/rgrove/sanitize
[dotenv-rails]: https://github.com/bkeepers/dotenv
