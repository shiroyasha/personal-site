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

# Loading code with `load`

The simplest way to load a file in ruby is to use `load`. It is simple,
robust, and in a way quiet dumb. Load simply loads and runs your code, 
nothing more, nothing less.

hello.rb

```ruby
def hello(name)
  puts "Hello #{name}! Have a nice day!"
end
```

main.rb

```ruby
load "/home/shiroyasha/examples/hello.rb"

hello("Patric") #=> "Hello Patric! Have a nice day!"
```

The previous example used the apsolute path to load you code, but you can
also use load with files in your current directory.

```ruby
load "./hello.rb"

hello("Sally") #=> "Hello Sally! Have a nice day!"
```

But, be aware, `load` will load you script even if it was already loaded.
This is probably not something you usually want, but it can come handy
when you want to reload your code if it changes while your script is running.

```ruby
load "./hello.rb" 

hello("Johny")

load "./hello.rb" # This will load "hello.rb" once again

hello("Testarosa")
```

You can also pass a second argument to the `load` method. It is boolean
value that tells the `load` method should it wrap your code in an anonymous
module.

At first glance this option can seem really unnecesarry, but it can protect
your code from the loaded one because all the variables are now preserved in that
anonymous module. You actully can't even use the loaded code. You can only run
it.

```ruby
load("./hello.rb", true)

hello("Natasha") # => no such method error
```

This can give you a hint that `load` isn't really meant to be used to load code,
but to write custom runners for your ruby code.

# Loading code with `require`

Unlike `load`, `require` loads your code a little smarter. It loads
your code only once and even tells you if your code was already loaded or not.

```ruby
require "hello"

hello("Jihny") # => true, the code was loaded

require "hello" # => false, the code was already loaded

hello("Testarosa")
```

As you can see, another neat thing about `require` is that it automatically adds
the ruby extension to the end of the file name. So you can load your code:

```ruby
# with a ruby extension
require "./hello.rb"
```

```ruby
# without a ruby extension
require "./hello"
```
