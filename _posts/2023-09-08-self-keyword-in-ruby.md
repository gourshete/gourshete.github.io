---
layout: post
title:  "What is self in Ruby?"
date:   2023-09-08
keywords: "ruby rails github learning swapnil gourshete ruby on rails self keyword"
image: assets/images/railsexamples-com-self.png
categories: [ Ruby ]
---

`self` is a keyword in ruby which means it is reserved by Ruby to serve a specific purpose and we cannot use it like regular variables (although you can override it, but you shouldn't).

## What is `self` in Ruby?
Behaviour of self depends on what context it is defined. `self` can represent instance of class or the class itself. Let's understand through examples.


### 1. within method
In this case, self represents the current instance of the class. It will be different for different instances of the class and will not intervene any proceedings between them.

##### Example 1:
```ruby
class RailsExamples
  def method1
    self.__id__
  end
end
```

```bash
irb(main):1:0> obj = RailsExamples.new
irb(main):2:0> obj.method1
irb(main):3:0> 460060
irb(main):4:0> 
irb(main):5:0> obj.__id__
irb(main):6:0> 460060
irb(main):7:0> 
irb(main):8:0> obj.method1 == RailsExamples.new.method1
irb(main):9:0> false
```

<br>

### 2. Within class
In this case `self` will represent the class itself. It will return the Class object under which it is defined. Let's understand through example -

##### Example 2:
```ruby
class RailsExamples
  def method1
    self.__id__
  end

  def self.method2
    self.__id__
  end
end
```

```bash
irb(main):1:0> RailsExamples.method2
=> 992600
irb(main):2:0> RailsExamples.method2
=> 992600
irb(main):3:0> RailsExamples.__id__
=> 992600
irb(main):4:0> RailsExamples.new.method1.__id__
=> 2052721
```

<br>

### 3. Outside any context
When `self` is called outside any class or method, it refers the main object (the top-level context).

```bash
irb(main):218:0> p self
main
=> main
```


Happy Coding!!!


---
References - 
 
- [keywords in Ruby](https://railsexamples.com/keywords-in-ruby/)
