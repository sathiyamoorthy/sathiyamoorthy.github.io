---
layout: post
title: "Ruby Newbies Useful Tips Part - I"
excerpt: "For Ruby newbies this post will be useful to learn tips and tricks of ruby and it contents the difference and approach of useful ruby codes."
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

### print vs puts vs p

Like other programming language Ruby also supports methods for printing information to the command line.

* `print` keyword will print the output in the same line.
* `puts` works like `print` but adds in next line and its intelligent enough to understand the escape character and act with the character 
* `p` is smarter than `print` and `puts` because it adds in next line and same time understand the object and `inspect` the object. 

Let's tweak with some example.

{% highlight ruby %}
#print will print the output in the same line
> print "Lets Geek "
> print "with print"
=> "Lets Geek with print" #print the output in the same line
#`puts` will print in the next line and its intelligent enough to understand the escape character and act with the character 
> puts "Lets geek"
> puts "with puts"
=> "Lets geek"
=> "with puts" # puts print the output as expected in the next line.
> puts "Lets \n Geek!”
=> “Lets”
=> “Geek!”
> puts "Tabs \t leave\tlong spaces" 
Tabs leave long spaces
=> nil
{% endhighlight %}
{% highlight ruby %}
#`p` is smarter than `print` and `puts` because it adds in next line and same time understand the object and `inspect` the object. 
> class Price
> def initialize(amt)
>  @amt=amt
> end
>end
> amt = Price.new(123)
> puts amt
=>#<Price:0x007faaf394b0d8> #puts didn't inspect the object
> p amt
=> #<Price:0x007faaf394b0d8 @amt=123> #p inspect the object
{% endhighlight %}

