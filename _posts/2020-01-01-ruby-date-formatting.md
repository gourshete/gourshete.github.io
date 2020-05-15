---
layout: post
title:  "Ruby date formatting"
date:   2020-01-01
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails database primary_key reset sequence
postgres"
image: assets/images/date-format.png
categories: [ Rails, Ruby ]
---

Ruby provides two classes to format date string `strftime` and `strptime`.

1. String to Date object

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

---

### Some methods provided by Date class

1. Find `end of the month`
```ruby
Date.parse('2020-01-01', '%Y-%m-%d').end_of_month
=> Fri, 31 Jan 2020
```

2. Find `end of the year`
```ruby
Date.parse('2020-01-01', '%Y-%m-%d').end_of_year
=> Thu, 31 Dec 2020
```

3. Find `day of the calender week`. Returns 1 to 7, Monday is 1 
```ruby
Date.parse('2020-01-01', '%Y-%m-%d').cday
=> 1
```

4. Find `day of the month`. 
```ruby
Date.parse('2020-01-01', '%Y-%m-%d').mday
=> 1
```

5. Find `week of the year`.
```ruby
Date.parse('2020-12-31', '%Y-%m-%d').cweek
=> 53
```

6. Find `day of the year`.
```ruby
Date.parse('2020-12-31', '%Y-%m-%d').yday
=> 366
```

7. Find `lilian day` number.
```ruby
Date.parse('2020-12-31', '%Y-%m-%d').ld
=> 160055
```

8. Find if given day is Sunday. Similar methods are available for all days of the week.
```ruby
Date.new(2020, 12, 31).sunday?
=> false
```

9. Find date after x days from the date
```ruby
Date.new(2020, 12, 31) + 8
=> Fri, 08 Jan 2021
```

10. Find date after x months from the date
```ruby
Date.new(2020, 12, 31) >> 8
=> Tue, 31 Aug 2021
```

...

- References

[Date.parse](https://apidock.com/ruby/v2_5_5/Date/parse/class) - [https://apidock.com/ruby/v2_5_5/Date/parse/class](https://apidock.com/ruby/v2_5_5/Date/parse/class)

[strptime](https://apidock.com/ruby/Date/strptime/class) - [https://apidock.com/ruby/Date/strptime/class](https://apidock.com/ruby/Date/strptime/class)

[strftime](https://apidock.com/ruby/Time/strftime) - [https://apidock.com/ruby/Time/strftime](https://apidock.com/ruby/Time/strftime)

[StackOverflow](https://stackoverflow.com/a/14619560/5235107) - [https://stackoverflow.com/a/14619560/5235107](https://stackoverflow.com/a/14619560/5235107)