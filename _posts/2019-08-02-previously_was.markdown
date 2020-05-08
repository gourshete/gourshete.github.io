---
layout: post
title:  "Rails 6 adds *_previously_was attributes method"
date:   2019-08-02
categories: [ Rails, new release ]
keywords: "rails github gryffindor learning swapnil gourshete rails6 ruby new release github _previously_was _previous_change
_previously_changed attribute_previously_changed active model swapnil gourshete"
---

Rails had `previous_changes` method to track value of object before and after save.

      person = Person.new(name: "Joe")
      person.name = "Bill"
      person.previous_changes         # => {"name" => ["Joe", "Bill"]}
      person.name_previously_changed? # => true
      person.name_previous_change     # => ["Joe", "Bill"]
      person.reload!
      person.previous_changes         # => {}

Now `*_previously_was` is added to the list. It adds attribute methods for each attribute in the `ActiveModel`.

In our case, `Person` has a attribute `name`. So it would be

      person.name_previously_was      # => "Joe"
      
For a pirate class object it will look like
      
      pirate.update(catchphrase: "Ahoy!")
      #Before
      pirate.previous_changes["catchphrase"] # => ["Thar She Blows!", "Ahoy!"]
      #Now
      pirate.catchphrase_previously_was # => "Thar She Blows!"

      
SOURCE :
<a href="https://github.com/rails/rails/pull/36836" target="_blank">commit</a>

Cheers!