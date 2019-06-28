---
layout: post
title:  "Modify a gem and use it in Rails"
date:   2019-06-28
---

Sometimes a situation arises where we need to modify a gem according to our requirement and then 
successfully integrate into our project. Let's find out!

<p>1. Download the repository of required gem from github.</p>

<p>2. Open codebase in any of the editor. Play with it(Rather make meaningful changes!).</p>

<p>3. Build gem locally. This is the most important STEP!!!<br>
Run `gem build foo.gemspec`<br>
This will create foo.gem file in the same directory. Remember the path of this directory.</p>

<p>4. In Gemfile put it down like<br>
gem 'foo', path: 'path/to/above/directory'</p>

<p>5. Run `bundle install`</p>

<p>And amigo you will be using the modified gem version.</p><br>

<h4>Note</h4> 
<p>This setup will be helpful, mostly for try and test approach.<br>
For a slightly better approach you can use github.</p>
<p>To use github, remember, the git source of gem must be specified.</p>
<p>3. In Gemfile put it down like<br>
gem 'foo', github: 'path/to/repository/relative/to/github', branch: 'your_branch'</p>

<p>4. Run `bundle install`</p>

<p>And you are off to the mark.</p>