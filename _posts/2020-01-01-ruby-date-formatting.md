---
layout: post
title:  "Ruby date formatting"
date:   2020-01-01
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails database primary_key reset sequence
postgres"
image: assets/images/date-format.png
categories: [ Rails ]
---

Ruby provides two classes to format date string `strftime` and `strptime`.

- String to Date object

Method `parse` of class `Date` converts string into date object with given directives. E.g.

```ruby
Date.parse('2020-01-01', '%Y-%m-%d')
```

The provided directives can be changed according to given string format.
```ruby
Date.parse('01-01-2020', '%m-%d-%Y')
=> Wed, 01 Jan 2020
Date.parse('31-01-2020', '%d-%m-%Y')
=> Fri, 31 Jan 2020
Date.parse('01/01/2020', '%m/%d/%Y')    
=> Wed, 01 Jan 2020
```

...

- References

[Date.parse](https://apidock.com/ruby/v2_5_5/Date/parse/class) - [https://apidock.com/ruby/v2_5_5/Date/parse/class](https://apidock.com/ruby/v2_5_5/Date/parse/class)

[strptime](https://apidock.com/ruby/Date/strptime/class) - [https://apidock.com/ruby/Date/strptime/class](https://apidock.com/ruby/Date/strptime/class)

[strftime](https://apidock.com/ruby/Time/strftime) - [https://apidock.com/ruby/Time/strftime](https://apidock.com/ruby/Time/strftime)

[StackOverflow](https://stackoverflow.com/a/14619560/5235107) - [https://stackoverflow.com/a/14619560/5235107](https://stackoverflow.com/a/14619560/5235107)