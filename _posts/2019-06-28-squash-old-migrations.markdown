---
layout: post
title:  "Squasher: Replacing old migrations"
date:   2019-06-28
---

Too many migrations in application makes it less interesting. Sometimes they are written a long time back, that 
now you do not even remember. At the point you might want to replace them with a new migrations.

<p>Rails have a gem for this utility, called <a href="https://github.com/jalkoby/squasher#readme">squasher</a>.
It eventually scans all the migrations in application and converts them into a single migration called SquashClean.
 Let's see by example.</p>

- Installation
 
<p>1. Include `gem squasher` in Gemfile and run bundle install.</p>

<p>2. To work effectively run `bundle binstub squasher` and you will have runner inside bin folder. 
Now we are set to use squasher</p>

- Usage

<p>3. Let's consider we need to squash all migrations before 2018. Simply 
 run `squasher 2018`<br>
and squasher will create single migration for all the migrations before 2018 and afterwards delete all those 
redundent migrations.</p>
<p> Yes it is that simple!</p>
<br>
<h4>Let's go down some depth</h4><br>
<p>Does Rails versioning affect our way?<br>
--> Yes. By default squasher will not generate any rails versioning for newly generated migration.</p>
<img src="{{ '/assets/img/squasher1.png' | prepend: site.baseurl }}" alt="">
<p>So there are high chances it may break during migrations.<br>
Simply squash comes with option - <br>
 -m, --migration=VERSION  define the rails migration version(since Rails 5)<br>
 It will rails versioning to the migration </p>
 <img src="{{ '/assets/img/squasher2.png' | prepend: site.baseurl }}" alt="">
