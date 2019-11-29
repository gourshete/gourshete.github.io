---
layout: post
title:  "Sidekiq By Example"
date:   2019-11-28
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails sidekiq background-jobs async"
---

What is the best way of handling background jobs in Rails, (maybe) using sidekiq.

Let's take step by step look into creating a Rails App and making a request for Background job using sidekiq

System Pre-requisite
* Ruby
* Rails
* Redis
* Sidekiq

<br>

### Create new Rails Project
We will create a new rails project named `sidekiq-example`

<img src="{{ '/assets/img/SS-sidekiq-new-project.png' | prepend: site.baseurl }}" alt=""> 


### Add sidekiq gem
In `Gemfile` add gem 'sidekiq'

`gem sidekiq`


Now run command `bundle install`. This will install gem sidekiq in our project.

`➜  sidekiq-example: bundle install` 

<br>

### Generate Model
Let's create a model named `Team` for reference with fields `name`, `rating`

<img src="{{ '/assets/img/SS-sidekiq-model.png' | prepend: site.baseurl }}" alt="">

Also add this in `seeds.rb`

<img src="{{ '/assets/img/SS-sidekiq-seed.png' | prepend: site.baseurl }}" alt="">

Now Run <br>
`➜  sidekiq-example: rails db:create && rails db:migrate && rails db:seed` <br>
It will create new database `sidekiq_example_development` for our application and create a table called `teams` in this database.
Running seed data will insert sample 5 records in it.

<br>

### Generate a controller
Create a controller for our actions under namespace `api/v1/`

<img src="{{ '/assets/img/SS-sidekiq-controller-1.png' | prepend: site.baseurl }}" alt="">

<br>

### Add routes
Let's add routes for our actions. Add this in `routes.rb`.

<img src="{{ '/assets/img/SS-sidekiq-routes.png' | prepend: site.baseurl }}" alt="">

<br>

### Add Sidekiq worker
Now let's work on Sidekiq part. To perform sidekiq jobs, add worker in `app/workers`. For our demo application
it is `BuyTimeWorker`. And add method named perform in it. When a call to `BuyTimeWorker` made, it will be a
asynchronous call to this method `perform`.

The logic for background job will be in this method `perform`. To keep it simple for now, will just add sleep timer 
in it.

<img src="{{ '/assets/img/SS-sidekiq-worker.png' | prepend: site.baseurl }}" alt="">

It simply sleeps for number of milliseconds passed to it. This job will run asynchronously when called.

Let's modify teams controller to make a call to this background job

<img src="{{ '/assets/img/SS-sidekiq-controller-2.png' | prepend: site.baseurl }}" alt="">

You can see action `show` is making call to `BuyTimeWorker`. What it means is when a url of kind `'/api/v1/teams/:id'`
is hit, the controller action `show` will get called and background job `BuyTimeWorker` will be triggered. The action `show`
will not wait for job `BuyTimeWorker` to complete though it is called from within its definition. This job will be 
executed asynchronously with method `show`.

<br>

### Run
* Start rails server
* Start Redis
* Start Sidekiq 

If you hit URL will found out something like this in sidekiq server log

`http://localhost:3001/api/v1/teams/2`

<img src="{{ '/assets/img/SS-sidekiq-server-log.png' | prepend: site.baseurl }}" alt="">


* ):

Well this is very simple example of running background job in rails. You can write complex logic in Sidekiq workers.

Cheers! 🍻🍻