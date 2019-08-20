---
layout: post
title:  "Ruby Ranges"
date:   2019-08-15
keywords: "ruby rails github gryffindor learning swapnil gourshete ranges sequence Range in ruby can be used in following situations
Sequence Range can be used to generate a sequence as simple as as Intervals as condition"
---

Range in ruby can be used in following situations

- as Sequence

Range can be used to generate a sequence as simple as `(1..100)` will generate a sequence from 1 to 100.
 
`array = (1..100).to_a`

will initialize an array of class Integer starting from 1 to 100. And it is easiest way to declare an array of sequence
in ruby.

- as Intervals

`if ((1..10) === 5)`
 
  `puts "5 lies in (1..10)"`

`end`

===>

5 lies in (1..10)


- as condition


      score = 70
      
      result = case score
         when 0..40 then "Fail"
         when 41..60 then "Pass"
         when 61..70 then "Pass with Merit"
         when 71..100 then "Pass with Distinction"
         else "Invalid Score"
      end
      
      puts result
      


Cheers!!!
