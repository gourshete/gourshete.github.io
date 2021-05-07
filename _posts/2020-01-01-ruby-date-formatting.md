---
layout: post
title:  "Ruby date formatting"
date:   2020-01-01
keywords: "ruby on rails database ruby date-formatting ruby rails github gryffindor learning swapnil gourshete postgres"
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

.

<h3>Format directives </h3>

```ruby
  %Y - Year with century (can be negative, 4 digits at least)
          -0001, 0000, 1995, 2009, 14292, etc.
  %C - year / 100 (round down.  20 in 2009)
  %y - year % 100 (00..99)

  %m - Month of the year, zero-padded (01..12)
          %_m  blank-padded ( 1..12)
          %-m  no-padded (1..12)
  %B - The full month name (``January'')
          %^B  uppercased (``JANUARY'')
  %b - The abbreviated month name (``Jan'')
          %^b  uppercased (``JAN'')
  %h - Equivalent to %b

  %d - Day of the month, zero-padded (01..31)
          %-d  no-padded (1..31)
  %e - Day of the month, blank-padded ( 1..31)

  %j - Day of the year (001..366)

Time (Hour, Minute, Second, Subsecond):
  %H - Hour of the day, 24-hour clock, zero-padded (00..23)
  %k - Hour of the day, 24-hour clock, blank-padded ( 0..23)
  %I - Hour of the day, 12-hour clock, zero-padded (01..12)
  %l - Hour of the day, 12-hour clock, blank-padded ( 1..12)
  %P - Meridian indicator, lowercase (``am'' or ``pm'')
  %p - Meridian indicator, uppercase (``AM'' or ``PM'')

  %M - Minute of the hour (00..59)

  %S - Second of the minute (00..60)

  %L - Millisecond of the second (000..999)
  %N - Fractional seconds digits, default is 9 digits (nanosecond)
          %3N  millisecond (3 digits)   %15N femtosecond (15 digits)
          %6N  microsecond (6 digits)   %18N attosecond  (18 digits)
          %9N  nanosecond  (9 digits)   %21N zeptosecond (21 digits)
          %12N picosecond (12 digits)   %24N yoctosecond (24 digits)

Time zone:
  %z - Time zone as hour and minute offset from UTC (e.g. +0900)
          %:z - hour and minute offset from UTC with a colon (e.g. +09:00)
          %::z - hour, minute and second offset from UTC (e.g. +09:00:00)
          %:::z - hour, minute and second offset from UTC
                                            (e.g. +09, +09:30, +09:30:30)
  %Z - Equivalent to %:z (e.g. +09:00)

Weekday:
  %A - The full weekday name (``Sunday'')
          %^A  uppercased (``SUNDAY'')
  %a - The abbreviated name (``Sun'')
          %^a  uppercased (``SUN'')
  %u - Day of the week (Monday is 1, 1..7)
  %w - Day of the week (Sunday is 0, 0..6)

Seconds since the Unix Epoch:
  %s - Number of seconds since 1970-01-01 00:00:00 UTC.
  %Q - Number of milliseconds since 1970-01-01 00:00:00 UTC.

Literal string:
  %n - Newline character (\n)
  %t - Tab character (\t)
  %% - Literal ``%'' character

Combination:
  %c - date and time (%a %b %e %T %Y)
  %D - Date (%m/%d/%y)
  %F - The ISO 8601 date format (%Y-%m-%d)
  %v - VMS date (%e-%b-%Y)
  %x - Same as %D
  %X - Same as %T
  %r - 12-hour time (%I:%M:%S %p)
  %R - 24-hour time (%H:%M)
  %T - 24-hour time (%H:%M:%S)
  %+ - date(1) (%a %b %e %H:%M:%S %Z %Y)
```

...

- References

[Date.parse](https://apidock.com/ruby/v2_5_5/Date/parse/class) - [https://apidock.com/ruby/v2_5_5/Date/parse/class](https://apidock.com/ruby/v2_5_5/Date/parse/class)

[strptime](https://apidock.com/ruby/Date/strptime/class) - [https://apidock.com/ruby/Date/strptime/class](https://apidock.com/ruby/Date/strptime/class)

[strftime](https://apidock.com/ruby/Time/strftime) - [https://apidock.com/ruby/Time/strftime](https://apidock.com/ruby/Time/strftime)

[StackOverflow](https://stackoverflow.com/a/14619560/5235107) - [https://stackoverflow.com/a/14619560/5235107](https://stackoverflow.com/a/14619560/5235107)
