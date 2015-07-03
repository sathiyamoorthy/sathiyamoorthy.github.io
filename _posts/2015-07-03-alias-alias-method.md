---
layout: post
title: "Rails alias vs alias_method vs alias_method_chain"
excerpt: "Differenece and approach between alias vs alias_method vs alias_method_chain"
date: 2015-07-03
status: publish
comments: true
share: true
categories:
- Rails 
tags:
- "Rails, Ruby, alias, alias_method, alias_method_chain, kishore-mohan, kishore.M, difference between alias vs alias_method vs alias_method_chain"
image:
  feature: technical_books.jpg
---

Before going to understand about the difference one should understand is this <b>method</b> or <b>keyword</b>. Believe most of them have this confusion because of the comma and passing argument to the alias we can't conclude its a method. Because **it's a Ruby keyword** (that trips every time we put a comma between the old and new method name,and the compiler complains).

Alias can be used in two contexts, Both class and instance level. But it must be inside the class either in self or on object level.

___
{% highlight ruby %}
User.class_eval{ alias :to_string :to_s }
> User.new.email.to_string #instance_method
=>"It works"

User.instance_eval{ alias :to_string :to_s }
>User.to_string #class_method
=>"User"
{% endhighlight %}
___

As a special case of the above, if "self" is a class, then you're
aliasing an existing method to a singleton method of the class - and a
singleton method of the class is what we usually call a class method.
That's why instance_eval()


Let's get into little basic example for the usage of **alias**:

{% highlight ruby linenos %}
class User
  def name
    "Let's Geek"
  end
 
  alias :label :name
end
 
User.new.label 
=> "Let's Geek"
{% endhighlight %}


OMG!! It works.. But where and why we need this alias. Lets put it into this way I want to refactor the application which loaded with lakhs of lines, better naming convention and override the method which we are going to see later part.

Now an example for the usage of alias_method:

{% highlight ruby linenos %}
class User
  def name
    "Let's Geek"
  end
 
  alias_method :label, :name
end
 
User.new.label 
=> "Let's Geek"
{% endhighlight %}

OOPS!! this also works and seems to be the same. except one comma(,) between the two methods. But the big difference is found in scoping. Here is the example with inheritance in both ways.

{% highlight ruby linenos %}
class ParentScope
  def foo
    "I am the Parent Scope"
  end
 
  alias :bar :foo
end

class ChildScope < ParentScope
  def foo
  	"I am the Child Scope"
  end
end

ChildScope.new.bar #=> "I am the Parent Scope"
ChildScope.new.foo #=> "I am the Child Scope"
{% endhighlight %}

Looks like ChildScope#bar points to the superclass #name method and not at ChildScope#foo! And this is the truth.

**alias_method** the convention says, a method and is executed in the current self scope.

{% highlight ruby linenos %}
class ParentScope
  def foo
    "I am the Parent Scope"
  end
 
  def self.apply_alias
    alias_method :bar, :foo
  end
end

class ChildScope < ParentScope
  def foo
  	"I am the Child Scope"
  end
  apply_alias
end


ParentScope.new.bar #=> "I am the Parent Scope"
ParentScope.new.foo #=> "I am the Parent Scope"
ChildScope.new.bar #=> "I am the Child Scope"
ChildScope.new.foo #=> "I am the Child Scope"
{% endhighlight %}

**alias_method** is executed the first time in the self scope of ParentScope and then the self scope of ChildScope and apply the method aliasing in the way we expected. While this looks like a tiny difference using alias_method grant more flexibility and may avoid unpredictable code behaviour.

### Difference between alias vs alias_method


   * alias_method is slightly more flexible accepting strings or symbols
   * alias_method will redefine local methods at runtime - which means you can override the aliased method in a subclass and alias_method will pick this up
   * alias will keep the original scope when aliasing - so even if you override the method in a subclass, the aliased method will refer to the parent's original method

### Get into alias_method_chain:
{% highlight ruby linenos %}

class MeetFriend
  def hi
    "Hi!!"
  end

  def hi_with_bye
  	"#{ hi_without_bye} and bye" 
  end

  alias_method_chain :hi, :bye
end

MeetFirend.new.hi #=> "Hi!! and bye"
MeetFirend.new.hi_without_bye #=> "Hi!!"
MeetFirend.new.hi_with_bye #=> "Hi!! and bye"
{% endhighlight %}

alias_method_chain behaves different than alias_method.


It overides the existing method, if want to acces without override should call ```MeetFirend.new.hi_without_bye``` then it triggers without overide.
When we want to override the gem existing methods with the your own behavior or injecting a variable into the existing method alias_method_cain will be very useful.

___
***Override Gem or Plugin with alias_method_chain***: 

{% highlight ruby linenos %}

  class Person
      def hello
        "Hello"
      end
    end

    module Flanderizer
      def self.included(base)
        base.class_eval do
          alias_method_chain :hello, :flanderizer
        end
      end

      def hello_with_flanderizer
        "#{hello_without_flanderizer}-diddly"
      end
    end

    # FOR FREEDOM!!!
    Person.send :include, Flanderizer

    flanders = Person.new

    flanders.hello # => "Hello-diddly"

    flanders.class.ancestors # => [Person, Flanderizer, Object, Kernel]
  {% endhighlight %}

___
***Difference between alias_method vs alias_method_chain***:

{% highlight ruby linenos %}

alias_method_chain :hello, :flanderizer

##which is equivalent to:

alias_method :hello_without_flanderizer, :hello
alias_method :hello, :hello_with_flanderizer

{% endhighlight %}
