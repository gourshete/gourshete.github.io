---
layout: post
title:  "Leetcode Valid Parenthesis Solution Ruby - 2"
date:   2023-09-28
keywords: "leetcode valid paranthesis ruby rails github learning swapnil gourshete"
image: assets/images/leetcode/leetcode-valid-parenthesis.png
categories: [ Ruby, Leetcode ]
tags: 'leetcode'
---

Problem Statement -

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

leetcode problem link - <a target="_blank" href="https://leetcode.com/problems/valid-parentheses/">valid-parentheses</a>

<br>

<h2>High level overview -</h2>

We need to tell if given sequence is a valid paranthesis. Goal here is to do it in O(n) time complexity and O(n) extra space.

We will iterate through each character, and check if any single opening bracket was processed for same set earlier. If yes, then we can mark this closing bracket as a pair for it and remove it from array list. Complete the processing of the input using same logic.

Now at the end we can decide if paranthesis is valid by looking at the content of the array - if it has any element at all it means the matching failed because either the closing bracket or opening bracket is in excess. If array is empty then we can safely say paranthesis is valid.

<br>

<h2>Algorithm -</h2>

1. Initiate an array to store the processed chars, initially empty
2. Iterate through each char
  1. check if it is closing bracket
    - if yes, check if closing bracket matches with last element in the array
  2. if no, then push the char to array
3. End loop
4. Check if the array is empty
  - yes? -> The input is a valid paranthesis
  - no? -> The input is not a valid paranthesis


<br>

<h2>Code -</h2>
```ruby
# @param {String} s
# @return {Boolean}
def is_valid(s)
  ar = []
  s.chars.each do |c|
    if (c == ')' && ar.last == '(') || (c == '}' && ar.last == '{') || (c == ']' && ar.last == '[')
      ar.pop
    else
      ar.push(c)
    end
  end

  ar.empty?
end
```

<br>

<h2>Benchmarking -</h2>

<span>Beats 80.09%of users with Ruby | Runtime : 59 ms</span>


<img src="{{ '/assets/images/leetcode/valid-paranthesis-1.png' | prepend: site.baseurl }}" alt="">


Happy Coding!!!