---
layout: post
title:  "Squasher: Replacing old migrations"
date:   2019-06-28
description: "Getting rid of old lengthy migration list is easy now. Squash all migrations into single one using
squasher gem. Let's see by example."
---

Too many migrations in application makes it painful. Sometimes they are written a long time back, that 
now you do not even remember. At the point you might want to replace them with something simple and compact.

<p>Rails have a gem for this utility, called <a href="https://github.com/jalkoby/squasher#readme" target="_blank"
>squasher</a>.
It eventually scans all the migrations in application and converts them into a single migration named InitSchema.
 Let's see by example.</p>

- Installation
1. Include `gem squasher` in Gemfile and run <br>`$ bundle install`
2. To work effectively run<br> `$ bundle binstub squasher` <br> and you will have runner inside bin folder. 

Now we are set to use squasher.

- Usage
1. Let's consider we need to squash all migrations before 2018. Simply 
 run <br>`$ squasher 2018`<br>
and squasher will create two migrations InitSchema and SquasherClean. InitSchema will be the new migration for all the 
migrations before 2018. Squasher afterward deletes all those now-redundent migrations.
<p> Yes it is that simple!</p>
<br>

### Let's go down some depth

- Does Rails versioning affect our way?<br>
--> Yes. By default squasher will not generate any rails versioning for newly generated migration.
<img src="{{ '/assets/img/squasher1.png' | prepend: site.baseurl }}" alt="">
So there are high chances it may break during migrations.<br>
To counter it, squasher simply comes with option - <br>
 `-m, --migration=VERSION`. It define the rails migration version(since Rails 5) 
<img src="{{ '/assets/img/squasher2.png' | prepend: site.baseurl }}" alt="">

<p></p>

- Can I squash migrations before a specific date?<br>
--> Yes. Simply run squash command like<br>
`$ squasher 2019/12/09`<br>
It will squash migrations before 09 December, 2019.