---
layout: post
title:  "Scopes in Rails"
date:   2018-07-07
keywords: "rails github gryffindor learning ruby scopes class method"
---

Recently I was calling create method on an active-record model object. But it failed in validation, because 
the provided foreign_key_id was not present in the associated table.
 
My first guess was it might be a dangling reference.
 But I was wrong. There was a record with this foreign_key_id in its table. So what went wrong? It was a problem with 
 `default scope` defined on an associated model.
 
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

That means instead of querying `Vehicle.where(color:'red')`, we would be simply doing

      Vehicle.red


The object returned by scope is always an `ActiveRecord::Relation` not `Array`. And this is the greatest benefit, because you can call all
the queries on this object just like any other `Relation` object.

      Vehicle.red
      Vehicle.red.count
      Vehicle.red.where(type: 'Hatchback')

`You should always pass a callable object to the scopes defined with #scope. This ensures that the scope is re-evaluated each
time it is called.`

.

### Default Scope

What if we need to query `Vehicle` model with some pre-fixed parameters. Suppose requirement is to show vehicles of drive type 
'Gear' only. We must add the `where(drive_type: 'Gear')` clause to all the requests. Is there a better way with scopes?

Yes!! 

Just by defining `default scope` we would be able to query the drive_type geared vehicles only. Just like

      class Vehicle < ActiveRecord::Base
        default_scope {where(drive_type: 'gear')}
      end
 
This will add `where(drive_type: 'gear')` to all the request we make to `Vehicle`.

This is just one way to use default scope. You can use default scopes `n` number of times in a Model. They all will be
club together in the resulting query.

      class Vehicle < ActiveRecord::Base
        default_scope {where(drive_type: 'gear')}
        default_scope {where(color: 'red')}
      end


In this way we are able to filter each request on Model with default scope.

..

### Unscoped

As much as we need `default scope`, we may also need to undo it at some places. It means calling a plain query on a Model without 
any pre-defined clause/s. It can be just like

      Vehicle.unscoped.count
      
It will result `Vehicle.count` by removing default clause `where(drive_type: 'gear')`

...

### How associations work with Scopes

Scopes have effect on associated classes. The default scope
will take effect when a parent class makes query to the associated class. Just like

      class Klass < ActiveRecord::Base
        has_many :vehicles
      end

      class Vehicle < ActiveRecord::Base
        belongs_to :klass
        default_scope {where(drive_type: 'gear')}
      end

When a query is made from `klass` object to `vehicles`, the default scope   `drive_type: 'gear'` will be auto considered.

....

### Diving Deep

Let's assume data for more clear picture

<img src="{{ '/assets/img/scopes_1.png' | prepend: site.baseurl }}" alt="">

Continue...

