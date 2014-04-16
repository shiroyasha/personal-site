---
title: From JavaScript to Ruby, Part 1
date: 2014-04-14
tags: example
disqus: 76563670-c5b9-11e3-9c1a-0800200c9a66
---

For more than 2 years now I have written almost all my applications in JavaScript or a similar JavaScript based language like CoffeeScript or LiveScript.
In the meantime I got quiet fond of the functional aspect of the language, the prototypes, and the unique way JavaScript handles objects and inheritance.

But as I transferred to a different company where the primary language is Ruby, I have started to adopt this strange little beast of a language. This is a tale of my quest to learn Ruby filled with moments of joy and frustration, and some interesting insights about the difference in the culture between the two.

# Blocks are not anonymous functions
The first thing I noticed is that people don't really like functions all that much as they like them in JavaScript.

Conversely they do like these things called blocks, an anonymous function like thing with a little more power then you would expect. And when I say a little more power I mean they can manipulate the scope they are inside of, for example:

``` javascript
function javascriptAnonymousFunctions() {
  [1, 2, 3, 4, 5].forEach(function(el) {
    console.log(el);
    return; // this return does nothing
  });
  console.log("I will be written out in the console");
}
```

``` ruby
def ruby_blocks
  [1, 2, 3, 4, 5].each do |el|
    puts el
    return # this returns from the ruby_blocks method
  end
  puts "I will NOT be written out in the console"
end
```

**Note:** To get the same behavior as in JavaScript you can of course prepend your block with _lamba_.

# Functions are better when they are shared

Of course in the above example the ruby version is more powerful and it gives you no example why I miss my functions in ruby. But, the beauty of functions could be only seen when they are reused and combined with other functions. For example:

``` javascript
var show = function(message) { console.log(message) }
var even = function(number) { return number % 2 == 0 }

var greaterThen = function(limit) {
  return function(number) {
    return number <= limit
  }
}

var lessThen = function(limit) {
  return function(number) {
    return number <= limit
  }
}

[1, 2, 3, 4, 5].map( show )

[1, 2, 3, 4, 5].filter( even ).map( show )

[1, 2, 3, 4, 5].filter( greaterThen(2) ).map( show )

[1, 2, 3, 4, 5].filter( greaterThen(2) )
               .filter( even )
               .filter( lessThen(5) )
               .map( show )

```

The same thing in ruby can't be written so easily, or at least not without confusing your colleges a little bit, or I have not learned enough Ruby yet to show you a quick and easy solution.

With this in mind, I still think that Ruby as a language rocks. There are dozens of shortcuts for every little thing you desire, and the syntax is clean and easy to understand. In the next part of my story I will try to focus on some of the awesome stuff I have found in this language.



