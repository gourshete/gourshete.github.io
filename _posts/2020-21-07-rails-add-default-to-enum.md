---
layout: post
title:  "Rails 6.0.3 - adds defaults value to enum"
date:   2020-07-04
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails defaults enum"
image: assets/images/rails-6.jpeg
categories: [ Rails, New addition, enum ]
---

How do we define enums? Pretty much like

```ruby
class Book < ActiveRecord::Base
  enum status: [:proposed, :written, :published]
end
```

Here what is the value of `status` for newly created object of class Book? It would be `proposed`, as is the first value 
from enums. What if we need a default enum value to be set to newly created objects?

Well we can achieve it using
database default value constraint, but it will not be assigned until object is saved to database i.e. `Book.new.status`
will not reflect `database default-value constraint` as it is yet to be saved to database.

- Rails added support to define default value for enum. Declaring like

```ruby
class Book < ActiveRecord::Base
  enum status: [:proposed, :written, :published], _default: :published
end
```

So now new object of class Book will show value for column `status` as `published` and not proposed.

```ruby
Book.new.status # => "published"
```

- More example

```ruby
class Blog < ActiveRecord::Base
  enum status: [:open, :inprogress, :complete], _default: :inprogress
end

Blog.new.status # => "inprogress"
```


<br>

Thanks for reading.

---

<br>

  References - 
 
- Rails [master PR](https://github.com/rails/rails/pull/39820) which adds _default enum by `kamipo`
