---
layout: post
title:  "Sidekiq By Example"
date:   2019-11-28
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response general"
---

What is the best way of handling background jobs in Rails, (maybe) using sidekiq.

Let's take step by step look into creating a Rails App and making a request for Background job using sidekiq

### Create new Rails Project
We will create a new rails project

<img src="{{ '/assets/img/SS-sidekiq-new-project.jpg' | prepend: site.baseurl }}" alt=""> 


### Add sidekiq gem
In `Gemfile` add gem 'sidekiq'

```ruby
gem sidekiq
```

Now run command `bundle install`. This will install gem sidekiq in our project.

### Generate Model

