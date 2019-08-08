---
layout: post
title:  "Useful Rails commands"
date:   2019-08-05
keywords: "rails github gryffindor learning swapnil gourshete rails6 ruby swapnil gourshete rails dbconsole rails runner rails notes The app and helper objects"
description: "There are a few commands that are absolutely critical to your everyday usage of Rails. In the order of how much you'll probably use them are: 
rails dbconsole rails runner rails notes The app and helper objects"
description_homepage: "rails dbconsole, rails runner, rails notes, app and helper objects"
---

---
* ### `rails dbconsole`

`rails dbconsole` figures out which database you're using and drops you into whichever command line interface you would use with it (and figures out the command line parameters to give to it, too!). It supports MySQL (including MariaDB), PostgreSQL, and SQLite3.

INFO: You can also use the alias "db" to invoke the dbconsole: `rails db`.

`$ rails dbconsole`



---
* ### `rails runner`

`runner` runs Ruby code in the context of Rails non-interactively. For instance:

`$ rails runner "Model.long_running_method"`

INFO: You can also use the alias "r" to invoke the runner: `rails r`.

You can specify the environment in which the `runner` command should operate using the `-e` switch.

`$ rails runner -e staging "Model.long_running_method"`

You can even execute ruby code written in a file with runner.

`$ rails runner lib/code_to_be_run.rb`


---
- ### `rails notes`

`rails notes` searches through your code for comments beginning with a specific keyword. You can refer to `rails notes --help` for information about usage.

By default, it will search in `app`, `config`, `db`, `lib`, and `test` directories for FIXME, OPTIMIZE, and TODO annotations in files with extension `.builder`, `.rb`, `.rake`, `.yml`, `.yaml`, `.ruby`, `.css`, `.js`, and `.erb`.

```bash
$ rails notes
app/controllers/admin/users_controller.rb:
  * [ 20] [TODO] any other way to do this?
  * [132] [FIXME] high priority for next deploy

lib/school.rb:
  * [ 13] [OPTIMIZE] refactor this code to make it faster
  * [ 17] [FIXME]
```

---
### The app and helper objects
 
 Inside the `rails console` you have access to the `app` and `helper` instances.
 
 With the `app` method you can access named route helpers, as well as do requests.
 
 ```bash
 >> app.root_path
 => "/"
 
 >> app.get _
 Started GET "/" for 127.0.0.1 at 2014-06-19 10:41:57 -0300
 ...
 ```
 
 With the `helper` method it is possible to access Rails and your application's helpers.
 
 ```bash
 >> helper.time_ago_in_words 30.days.ago
 => "about 1 month"
 
 >> helper.my_custom_helper
 => "my custom helper"
 ```
 
`Cheers!!!`