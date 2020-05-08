---
layout: post
title:  "Reset primary key sequence"
date:   2020-04-16
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails database primary_key reset sequence
postgres"
image: assets/images/reset_pk.jpg
categories: [ Rails, Postgres, Database ]
---

Resetting primary key sequence in Rails can be achieved by simply calling method `reset_pk_sequence!` on ActiveRecord with 
`table_name`.

```ruby
  ActiveRecord::Base.connection.reset_pk_sequence!('table_name')
```


- What is Primary key sequence?

It is a value maintained by database, which it refers to when adding new row. This is used to decide next value for primary key column. In 
most common scenario the column named `id` holds primary key for the table. 

When first row is being added, `id` is set to **1**. At this time id_sequence would be `2`. When second row is added, id_sequence would be
set to `3` and likewise.

- Why to reset this sequence?

Sometimes due to imported records or other reason, id_sequence is not updated to hold the right value. Suppose we imported 10 records 
to the above schema with their ids from previous schema and those ids not conflicting with existing 2 records. And id_sequence is not
updated.

Now the value of id_sequence is `3`, at the same time record with id **3** is present(from imported records). In this case, 
database insert operation will fail with error `duplicate primary key - validation failure`.

- How to reset?

Open database console and run 

```bash
SELECT setval('your_table_id_seq', COALESCE((SELECT MAX(id)+1 FROM your_table), 1), false);
```

- How to reset from Rails console?

```ruby
  ActiveRecord::Base.connection.reset_pk_sequence!('table_name')
```

- How to reset for all tables?

```ruby
ActiveRecord::Base.connection.tables.each do |t|
  ActiveRecord::Base.connection.reset_pk_sequence!(t)
end
```

...

* References - 

[StackOverflow](https://stackoverflow.com/a/244265) - [https://stackoverflow.com/a/244265](https://stackoverflow.com/a/244265)

[Rubyinrails](https://rubyinrails.com/2019/07/12/postgres-reset-sequence-to-max-id-in-rails/) - [https://rubyinrails.com/2019/07/12/postgres-reset-sequence-to-max-id-in-rails/](https://rubyinrails.com/2019/07/12/postgres-reset-sequence-to-max-id-in-rails/)
