---
layout: post
title:  "Leetcode Valid Anagram Solution Ruby - 3"
date:   2023-09-28
keywords: "leetcode valid anagram ruby rails"
image: assets/images/leetcode/leetcode-3-cover-1.png
categories: [ Ruby, Leetcode ]
tags: 'leetcode'
---

Problem Statement -

Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

leetcode problem link - <a target="_blank" href="https://leetcode.com/problems/valid-anagram/">Valid Anagram</a>

<br>

<h2>High level overview -</h2>

We need to tell if given sequence is a valid anagram. Goal here is to do it in O(n+m) time complexity and O(n+m) extra space.

We will iterate through each character of both strings and keep track of how many times it has appeared.

But How to store the count? What is best suited data structure?
Hash will be ideal data structure for this use case, where key will be char and value will be their respective count. And of course, we will need two hashes.

Then we will compare these two count values and decide if it is a valid anagram. If they both match, then it is valid. If they do not match, then it is invalid.

Choices -

As problem statement says - *using all the original letters exactly once*, we can also solve it using sort.
Sort both strings and then compare them. But sort will take O(nlogn) complexity, whereas above approach will take O(n+m) time.

<br>

<h2>Algorithm -</h2>

1. Count occurrances of each char using `.tally` method. It will return `hash` object
2. Check if both the hash objects match
  - yes? -> The input is a valid anagram
  - no? -> The input is not a valid anagram


<br>

<h2>Code -</h2>
```ruby
# @param {String} s
# @param {String} t
# @return {Boolean}
def is_anagram(s, t)
  return false if s.length != t.length

  s.chars.tally == t.chars.tally
end
```

<br>

<h2>Benchmarking -</h2>

<span>Beats 80.09%of users with Ruby | Runtime : 59 ms</span>


<img src="{{ '/assets/images/leetcode/leetcode-3-bc.png' | prepend: site.baseurl }}" alt="">


Happy Coding!!!