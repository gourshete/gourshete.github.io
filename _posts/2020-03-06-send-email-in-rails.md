---
layout: post
title:  "Sending Email in Rails"
date:   2020-03-06
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails sidekiq background-jobs async"
---

Sending email is almost integral part of every web application nowadays. In this post we will cover how to send emails
from a rails application.

First you need an active smtp server to send an email, because only SMTP servers are capable of sending or receiving emails.
There are many providers such as gmail, sendgrid and more. For this post, we will consider using gmail.

Assuming you have a Rails application with User model.

- We need to configure SMTP server. This can be set in config/environments/development.rb

```ruby
  config.action_mailer.delivery_method = :smtp
  host = 'example.com' #replace with your own url
  config.action_mailer.default_url_options = { host: host }

  # SMTP settings for gmail
  config.action_mailer.smtp_settings = {
      :address              => "smtp.gmail.com",
      :port                 => 587,
      :user_name            => ENV['EMAIL'],
      :password             => ENV['PASSWORD'],
      :authentication       => "plain",
      :enable_starttls_auto => true
  }
```

- Let's write the code now. What will be sent in the email? Let's say we want to send a welcome mail when user signs up.
We will generate a mailer named - 
rails g mailer UserRegistration <br>
This will generate 
<img src="{{ '/assets/img/SS-send-email-1.png' | prepend: site.baseurl }}" alt="">

- Open app/mailers/user_registrations_mailer.rb and add method following method 
```ruby
def registration(user)
    @user = user
    mail(to: user.email, subject: 'Welcome to Rails learning')
end
```
- Open `app/views/user_registrations_mailer` & add a new .erb file whose name resembles with method name in 
`app/mailers/user_registrations_mailer.rb`. In our case it is `registration.html.erb`, now put in whatever welcome message 
you want a user to see in email. I will simply add

Hello <%= @user.first_name%> <%= @user.last_name %>,

Welcome to Ruby on Rails learning.

Thanks for signing up.


- We need to trigger the action of sending emails. There are multiple ways to achieve this. Can call this from controller 
action or a service call or activerecord callback. Will prefer last option here
In `User` model register `after_create` callback

```ruby
after_create :send_sign_up_email
.
.
.
private
def user_registration_email
  UserRegistrationsMailer.registration(self).deliver_now
end
```


And now you are all set to send sign-up emails.