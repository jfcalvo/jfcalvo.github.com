---
type: post
layout: default
title: Default values and hash arguments with Ruby
summary: How to add default values to optional hash arguments with Ruby methods.
language: english
---

A common and idiomatic solution to the lack of keyword arguments in Ruby methods is the use of hashes. This pattern is used a lot inside Rails and other frameworks.

{% highlight ruby %}
def search(type, options = {})
  # ...
end

search :people, age: 40, country: 'spain'
{% endhighlight %}

But how can we add default values to the `options` hash argument?. Rails included a useful method in the `Hash` class called [`reverse_merge!`](http://api.rubyonrails.org/v2.3.8/classes/ActiveSupport/CoreExtensions/Hash/ReverseMerge.html) that we will use to add default values to our `options` hash argument. Assuming that we need the next following default values: `age: 20, country: 'france'` the search method will be as follow:

{% highlight ruby %}
# With Rails (using reverse_merge!)
def search(type, options = {})
  options.reverse_merge! age: 20, country: 'france'
  # ...
end
{% endhighlight %}

If you are not using Rails you will not have `reverse_merge!` included in `Hash` class so you will need to use other solution, in this case we will use the [`merge`](http://www.ruby-doc.org/core-1.9.3/Hash.html#method-i-merge) method with the default hash to not losing the possible values indicated in the `options` argument:

{% highlight ruby %}
# Without Rails (using merge)
def search(type, options = {})
  options = { age: 20, country: 'france' }.merge(options)
  # ...
end
{% endhighlight %}

The approach to the problem using `reverse_merge!` method is by far more readable and elegant that the version using `merge`. Perhaps would be a good idea to add this method to the Ruby Core `Hash` class. Anyway [Ruby 2.0 will include keyword arguments](http://ruby-dev.info/posts/44602) and all of this will be unnecessary (or different).
