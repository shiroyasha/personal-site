---
title: Actions and transformations in OOP based design
date: 2014-04-19
disqus: 64cb3f84-c22d-46f3-9b1f-1045fa2478c0
published: true
---

Object oriented programming comes so naturally when I am modeling real life
stuff, or creating abstract data types. But there is a whole range of problems
that are really hard to express using objects, or at least they are hard for me.
READMORE

``` ruby
# example of real life thing
def Dog
  def initialize(name)
    @name = name
  end

  def bark
    puts "bark"
  end
end
```

``` ruby
# example of abstract data type
def Stack
  def initialize
    @stack = []
  end

  def push(thing)
    @stack.unshift(thing)
  end

  def pop
    @stack.shift()
  end
end
```

# Representing actions
This is a problem I come across every so often. There are tasks where I have
to __do__ something. To show a list, to send some data to the server, to
calculate some value, to filter some things. And there are a lot of ways to
resolve these problems. Most of them are incorrect, some of them are weird, but
all of them are somehow unnatural in an pure object oriented environment.

# Solution 1: Create a class for everything
In the purest object oriented methodology I would address the above problems
by trying to find or invent a subject that will perform my actions. Then by
defining  a method in the subject I would implement my desired behavior.

For example if I want to send some data to the server I could write:

``` ruby
def DataSender
  def initiallize(server, data)
     @server = server
     @data = data
  end

  def send
     json = {
        :title => "Hello server",
        :body => @data["value"],
        :password => "keyboard kat"
    }
    client = HttpClient.new(server.ip_address, :port => 4567)
    client.send(json)
  end
end

data = { :value => "nice to meet you" }
sender = DataSender.new my_server, data
sender.send()
```

But this is so weird, and unnatural I would say. Because the original thing
I wanted to do is to __send__ some __things__. The notion of a __DataSender__
is artificial and creates an abstraction that doesn't give me more power and
neither does it take away from the complexity of the original problem.

__In fact it is an abstraction solely created for the sake of abstracting__.
And abstractions lead to greater complexity, and also they create a harder
and more confusing environment for maintenance.

# Solution 2: Put the send method inside the Server class

A different solution would be to put my send method inside the server's
class, and maybe to rename it a little to something like __recieve__.

``` ruby
def Server
   def initialize(ip_address)
     @ip_address = ip_address
   end

   # ...

   def recieve
      # something similiar as above
   end
end
```
But there is a problem. I can now only create servers which must be able to
send out data. And usually this is not the case, because there are a lot of
servers from which I only want to read out data. Of course I could create a
__could_recieve?__ method, but then I would need to check it every time
before I send out something.

The other solution is to create an inherited class named something like
__ServerThatICanSendTo__. But the name alone tells you that this is a
wrong path to take. So it seems that putting the __send__ method inside
of the server class is a wrong idea after all.

# Solution 3: Creating static methods to deal with actions
This is usually the way I handle these kind of problems in the object
oriented world. By creating a static method I am only connecting an action
with a namespace and I don't artificially create an abstraction for
performing an action. But where should I put this static method?

* Inside a subject?
* Inside some collection of utility methods that are probably not even
connected in any way?
* Or should I create some kind of a namespace wrapper for a collection
of connected utility methods?

I don't know. I frankly I don't even like to think about this problem
too much, as it is obvious to me that there is no clear way of handling my
problems in an object oriented way.

The point of this way too long post is that _the object oriented paradigm
doesn't provide an easy and bulletproof way of handling utility methods
such as actions and transformations of data_.

But as always, I am perhaps/probably wrong. Feel free to correct me or to
show me an awesome solution.
