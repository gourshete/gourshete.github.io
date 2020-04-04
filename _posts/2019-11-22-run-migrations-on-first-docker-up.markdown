---
layout: post
title:  "Run seed data only on first Docker instance up"
date:   2019-11-22
categories: [ Rails ]
keywords: "ruby rails github gryffindor learning swapnil gourshete migration docker kubernetes circleci bash devops"
---

Q: Do we need to run rails db:seed, rails db:migrate every time the deployment happen? <br>
**Ans -** Absolutely no. rails db:seed should only run for the first time i.e. first deployment. But migrations should
be run on every deployments. 

So here is what we need **-** Run seed data only for first deployment. We will consider here containerised architecture.

**Here are steps -** <br> 
During deployment
* Check if db exists
* If yes, then run rails db:migrate
* If no, then run rails db:create && rails db:migrate && rails db:seed

<br>

#### How to determine if db exists during deployment? <br>
**Ans -** After some googling, found out that a rake task can be written to determine if db exists

```ruby

    namespace :db do
      desc "Checks to see if the database exists"
      task :exists do
        begin
          Rake::Task['environment'].invoke
          ActiveRecord::Base.connection
        rescue
          exit 1
        else
          exit 0
        end
      end
    end    

```

This task tries to establish connection with the database, if exception occurs then return with exit 1. Exception
occurred, here, means the database does not exists. And no exception means connection established successfully and
return with exit 0. To summarise, 

```bash
    if db does not exists then exit 1
    if db exists then exit 0
```
 
<br>
#### Run seed data if db:exists, How? <br>
**Ans -** In deployment script, the conditional bash logic can be executed like 

     args: [ "-c", "env && bundle exec rake db:exists; DB_EXISTS=$?;  [[ $DB_EXISTS = 1 ]] && (rails db:create db:migrate db:seed) || (rails db:migrate)" ]

`bundle exec rake db:exists; DB_EXISTS=$?;  [[ $DB_EXISTS = 1 ]] && (rails db:create db:migrate db:seed) || (rails db:migrate)` <br>
This makes call to rake task above. Then collects its output into a variable DB_EXISTS. Then check if value of DB_EXISTS is equal to 1(which means db does not
exists, according to our above assessment), IF YES THEN RUN `rails db:create db:migrate db:seed`, ELSE run `rails db:migrate`.


Cheers! 🍻🍻