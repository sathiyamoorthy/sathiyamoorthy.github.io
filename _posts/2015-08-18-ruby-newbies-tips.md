---
layout: post
title: "Ruby Newbies Useful Tips"
excerpt: "For Ruby newbies this post will be useful to learn tips and tricks of ruby and it contents the difference and approach of using useful ruby codes."
date: 2015-08-18
status: publish
comments: true
share: true
categories:
- Ruby
tags:
- "Ruby, Newbies, String, Hash, irb, kishore-mohan, kishore.M"
image:
  feature: ruby.jpg
---

### Underscore( _ ) magic in console or irb
Underscore(_) is a special magic varibale works in console or irb, which takes the last execution values int the `_` variables automatically. If you want to use the last obtained output you can do so by using underscore `_` as a variable.

___
{% highlight ruby %}
> "hi" 
=> "hi"
> _ + " Let's"
=> "hi Let's"
> _ + " Geek"
=> "hi Let's Geek"

{% endhighlight %}
___
{% highlight ruby %}
> 5 
=> 5
> _ * 10
=> 50
{% endhighlight %}

Without storing the value into some variable, last execution value can be easily used from `_`.

###Single quotes(' ') & double quotes(" ") difference

Both work very similar and even on perfomance not much difference between single and double quotes. 
Double quotes `" "` used where we want to use string `interpolation`.
___
{% highlight ruby %}
#both return similar value
> ''.class
=> String
> "".class
=> String
> "lets Geek"
=> "lets Geek"
> 'lets Geek'
=> "lets Geek" 
#single and double quote with Interpolation
> g = "Geek"
> "lets #{g}" #interpolation
=> "lets Geek"
> 'lets #{g}'
=> 'lets \#{g}' #single quote return with escape sequence
{% endhighlight %}
___

Interpolation - Variable can embed it into a string by putting it like `#{put_your_variable_here}`


In the above example we can see the single quote gets printed as it is instead of giving the variable value as double quotes works.