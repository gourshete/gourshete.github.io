---
layout: post
title:  "Scopes in Rails"
date:   2018-07-07
keywords: "rails github gryffindor learning ruby scopes class method"
---

Recently I was calling create method on an active-record model object. But it failed in validation, because 
the provided foreign_key_id was not present in the associated table. My first guess was it might be a dangling reference.
 But I was wrong. There was a record with this foreign_key_id in its table.
 
 Let's first understand how scopes work in Rails. When we define a scope on an ActiveRecord model
      
      class Vehicle < ActiveRecord::Base
        scope :red, -> { where(color: 'red') }
      end
 
 a class method is added to the Model. It is simply like this

      class Vehicle < ActiveRecord::Base
        def self.red
          where(color:'red')
        end
      end

The object returned by scope is always an `ActiveRecord::Relation` not `Array`. And this is the greatest benefit, you can call all
the queries on this object just like any other `Relation` object.

      Vehicle.red
      Vehicle.red.count
      Vehicle.red.where(type: 'Hatchback')

`You should always pass a callable object to the scopes defined with #scope. This ensures that the scope is re-evaluated each
time it is called.`

 
Let's assume data for more clear picture

<img src="{{ '/assets/img/scopes_1.png' | prepend: site.baseurl }}" alt="">

