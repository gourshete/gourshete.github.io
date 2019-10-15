---
layout: post
title:  "Asset Pipeline"
date:   2019-08-24
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails asset pipeline"
---

It functions mainly in 3 parts - 
1. Concatenation
2. Compression
3. Support higher level languages 

Fingerprint - 

Rails automatically appends fingerprint at the end of file names based on its content, previously was date based.


Why precompile assets?
--> In the world of internet, speed is much weighted factor. Browsers consumes some real time when it makes so many requests 
from single html page for its assets to load. Asset pipeline minimises this time by concatenating some of these javascript and css
files. 
