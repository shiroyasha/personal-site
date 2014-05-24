---
title: Loading ruby code
date: 2014-05-23
disqus: 146d77c1-2ca9-461a-a561-d3695956e449
published: false
---

While you are using a nice and confy rails environment, where
everything you need is already loaded for you, you don't really
worry about loading your code. But, the moment you want to write
a pure ruby script or do something outside of a rails environment
the problems with code loading get really obvious and frustrating.
Writting anything more involved without some code loading 
strategie is a certain way to get lost in you project.

So... how do we load code in ruby? Well... there are lots of ways
to load code in ruby, and it depends on what you want to achive 
and how you want to structure your script.

#Loading code with `load`

The simplest way to load a file in ruby is to use `load`. It is simple,
robust, and in a way quiet dumb. Load simply loads you code, nothing more
nothing less.

hello.rb

```ruby
def hello(name)
  puts "Hello #{name}! Have a nice day!"
end
```

main.rb

```ruby
load "hello.rb"

hello("Patric") #=> "Hello Patric! Have a nice day!"
```

But, be aware, `load` will load you script even if it was already loaded.
This is probably not something you usually want, but it can come handy
when you want to reload your code if it changes while your script is running.

```ruby
load "hello.rb" 

hello("Johny")

load "hello.rb" # This will load "hello.rb" once again

hello("Testarosa")
```
