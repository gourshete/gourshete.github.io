---
layout: post
title:  "String Comparison: StringInquirer"
date:   2019-07-07
keywords: "rails github gryffindor learning ruby string comparison eql equal StringInquirer"
image: assets/images/equality.png
categories: [ Rails, Ruby ]
---

Generally we use `==/===/eql?/equal?` for string comparison in Rails.
It does work in all scenarios we needed. But we often tend to look how same things can be done in more clean ways or how other developers in Rails
community would have done that.


``` ruby
str = 'x'

str.eql?'X'
str.equal?'X'
str=='X'
str==='X'
```

The best place to look for such examples, in my opinion, is Rails repository on github itself. 

Let's see how string comparison is done by Rails community inside Rails core code.

There is a class in place called <a href="https://github.com/rails/rails/blob/master/activesupport/lib/active_support/string_inquirer.rb" target="_blank">`StringInquirer`</a>.

Wrapping a string in this class gives you a prettier way to test for equality. The value returned by <tt>Rails.env</tt> is wrapped in a 
StringInquirer object, so instead of calling this:

    Rails.env == 'production'
  
  you can call this:
 
    Rails.env.production?
 
  Instantiating a new StringInquirer
 
    user = ActiveSupport::StringInquirer.new('admin')
    user.admin?   # => true
    user.admin?  # => false
    
Cheers!