---
title: From Javascript to Ruby, Part 1.5
date: 2014-04-18
disqus: b079b91c-f47a-4a33-abb4-0d65c7fcbd08
published: true
---

This post is a continuation of [From Javascript to Ruby, Part 1](/posts/from-javascript-to-ruby-part-1.html), and also an answer to [@dear_gamemaster](https://twitter.com/dear_gamemaster)'s blog [post](http://www.pixelablaze.com/re-from-javascript-to-ruby/)
READMORE

# Extending classes is an antipattern

I really like your first example, and for a small application that can be
in fact a viable solution. But as my application grows the need for some
utility functions/methods will probably scyrocket, and with this
approach I would effectively create public global methods, available in all the parts of my application, and I did not even mention the possible name collisions that I and my team members could easily make.

# Extending classes locally

What would really be nice is to have a mechanism that would allow me to
extend a class or an instance locally or bound to some scope. That
way all the problems regarding name collisions and gloabal method polution
would magically fade away. For example, this would be really nifty:

``` ruby
module ArrayPowerups
  def between(a, b)
    select { |x| x > a && x < b }
  end

  def even
    select { |x| x.even? }
  end
end

def calulate(a, b)
  Array.extend_locally_with(ArrayPowerups)

  [1,2,3,4,5].between(a, b).even
end

[1,2,3,4,5].even # => NoMethodError
```

Unfortunatelly, I think there is no programming language that would provide this functionality out of the box. Maybe there is a good reason behind it?

# The third solution, a.k.a use what you alrady have

``` ruby
[1,2,3,4,5].select { |x| x.between?(3, 5) and x.even? }
```

This is only good if I have all the functionality needed already prepared
for me. Most of the time this isn't true, but would be really great if it would.

# Using blocks and procs

When I look at your code example I can see almost identical behaviour
expressed with totally different implementation. I am of course talking
about `show` and `lessThen`. They are both methods, both of them do
things, but one is "wierd" and the other is "normal" when I consider
they implementation.

The other more important thing is, I can't call show as a normal function.

``` ruby
show = Proc.new { |msg| puts msg }

show "Hello world!" # This does not work
```

That really bugs me. I can't reuse my methods as efficiently as
in Javascript. Or I would create a normal method, and a Proc which invokes that method.

``` ruby
def show(msg)
  puts msg
end

show_proc = Proc.new { |msg| show(msg) }

show("Hello world") # works
[1,2,3,4,5].each(&:show) # this also works
```

Alternatively, I could use this really unconfortable syntax and write

``` ruby
def show(msg)
  puts msg
end

[1,2,3,4,5].each(&method(:show))
```

But I can't do the same with less_then if I wan't to use it's returned method as I would use a normal method.
