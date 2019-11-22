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

Support higher languages - 
Assets pipeline can convert code from higher level languages like .erb, coffeescript into respective css and js. So if we are writing
in a file with extension css.erb, all helper methods become available in this file. I can write 

    .div {
      url: "<%= asset_path %>/div-image";
    }

Fingerprint - 
Rails automatically appends fingerprint at the end of file names based on its content, previously was date based.


Why precompile assets?
--> In the world of internet, speed is much weighted factor. Browsers consumes some real time when it makes so many requests 
from single html page for its assets to load. Asset pipeline minimises this time by concatenating some of these javascript and css
files. 
