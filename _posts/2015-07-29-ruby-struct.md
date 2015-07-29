---
layout: post
title: "Why struct? Not Hash or OpenStruct?"
excerpt: "When we want to store the key value pair most of them prefer Hash, because that is how we learned from the basic. But in real time compare to Hash and Openstruct, Struct works better than other key value storage."
date: 2015-07-29
status: publish
comments: true
share: true
categories:
- Ruby 
tags:
- "Ruby, Struct, Ruby Hash, Ruby Openstruch, Ruby Struct, kishore-mohan, kishore.M, difference between struct vs openstruct vs hash, Why Struct? Not Openstruct or Hash?"
---

Most of them prefer Hash when we want to store the object with key and value pair, because that's how we learned ruby basics. When we keeping growing we will be well attached with hashes and start dumping the hash concept everywhere.

Eventually, most of them believe that hashes behave more like objects and easy to use, but this is a horrible idea. Let's conclude this in a short while.

###alien! code - Based on the view and approach(Hash)
___
{% highlight ruby %}
def result(status, value)
  result= {}
  result["status"] = status
  result["value"] = value
  result
end

> r = result("success", 2)  
> r["status"] => "success"
> r["value"] => 2
> r[:status] => nil #symbol and string conflict
> r[:types] => nil #Developers likes "typo" and not giving any exception
{% endhighlight %}
___

Hashes in ruby are loosley related data structue, it doesn't provide any exception on both getter and setter. Again the biggest challenge between get the values from hashes depends on symbol and string on keys.


Hash can be very useful when storing dyanmic keys using some logic, number of keys are not constant and non structured data. But when the keys are constant and structured data, storing with hashes like putting your code into non scalable and vulnerable. Alien!! 

{% highlight ruby %}
class Result
  attr_accessor :status, :value
  def initialize(status, value)
    @status = status
    @value = value
  end
end

> result = Result.new("success", 2)
> result.status = "success"
> result.value = 2
> result.types 
NoMethodError: undefined method `status' for #<Result:0x007fd1689ecfa0 @status="success", @value=2>s
{% endhighlight %}

Sometimes we likely to be said, "can hashes accessed like an object" the above code more looks like developer friendly and can access as a object easily get and set values from object. But it can be frustrated creating a class and initializing the variable which doesn't make sense writting two many lines.

###OpenStruct - Killer with flexible hands

We will found OpenStruct, it solves the problem of hash key lookup by providing them as methods and easy to access. Looks pretty close to hash but it is missing many methods which hash supports.
___
{% highlight ruby %}
require "ostruct"
result = OpenStruct.new(status: "success", value: 2)

> result.status = "success"
> result.value = 2
> result.status = nil # Typo or undefined keys, not give any exception
{% endhighlight %}
___

But OpenStruct perfomance was seriously bad!! its very slower than hash, because OpenStruct uses ruby **method_missing** and **define_method** to generate dynamic methods and going with metaprogramming code something should think its really necessary. 

###Struct - Finally!!

Struct works very similar like OpenStruct, except that it will not support dynamic undefined attributes and should follow class naming convention.

___
{% highlight ruby %}
Result = Struct.new(:status, :value)

> result = Result.new("success", 2)
> result.status = "success"
> result.value = 2
> result.types 
NoMethodError: undefined method `types' for #<struct Result status="success", value=2>

# or 
class Result < Struct.new(:status, :value)
end

#both are same 
{% endhighlight %}

___

Struct is faster than Hash and OpenStruct, very reliable and readable code.




