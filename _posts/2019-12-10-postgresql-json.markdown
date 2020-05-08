---
layout: post
title:  "json and jsonb - Postgresql"
date:   2019-12-10
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails postgresql json jsonb"
categories: [ Rails, Postgres ]
---

Postgresql provides a data-type `jsonb` to save data from JSON format. There are two ways for it - using `json`
and `jsonb`. This article will clarify difference in short terms.

`json` and `jsonb` are very similar to each other. The key difference is - `jsonb` is binary representation of `json` -
as per postgresql documentation.

- Pros -  `jsonb`

1. Improved efficiency
2. Postgresql provides query interface for these types. So a direct query for any key in column can be made.
3. Simple database schema

- Cons -  `jsonb`

1. Slight overhead to convert into binary form.
2. Aggregate queries are slower (due to lack of statistics).
3. Due to large table footprints may take large disk space.

...

#### Querying json field

1. `Creating table` 
```postgresql
create table foo (id serial NOT NULL primary key, metadata json)
```

2. `inserting test data` 
```postgresql
insert into foo(metadata) values ('{ "property": "bar1" }'), ('{ "property": "bar2" }')
```

3. `fetching data from table foo`
```postgresql
select * from foo
```
<img src="{{ '/assets/images/select-foo.png' | prepend: site.baseurl }}" alt="">

4. `selecting json field`
```postgresql
select id, metadata ->'property' as property from foo
```
<img src="{{ '/assets/images/select-property.png' | prepend: site.baseurl }}" alt="">

Cheers!!!