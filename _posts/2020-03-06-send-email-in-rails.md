---
layout: post
title:  "Sending Email in Rails"
date:   2020-03-06
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails sidekiq background-jobs async"
---

Sending email is almost integral part of every web application nowadays. In this post we will cover how to send emails
from a rails application.

First you need an active smtp server to send an email, because only SMTP servers are capable of sending or receiving emails.
There are many providers such as gmail, sendgrid and more. For this post, we will consider using sendgrid.

Assuming you have a Rails application with User model.

1. Check the following settings are set in devise.rb
 
config.mailer = 'DeviseMailer'

config.mailer_sender = 'support@yourdomain.com'

2. Now we need to configure SMTP server. This can be set in config/initializers/mail.rb

```ruby
ActionMailer::Base.delivery_method = :smtp
ActionMailer::Base.smtp_settings = {
    :user_name => SENDGRID_USERNAME,
    :password => SENDGRID_PASSWORD,
    :domain => MAILER_HOST,
    :address => 'smtp.sendgrid.net',
    :port => 587,
    :authentication => :plain,
    :enable_starttls_auto => true
} 
```

3. Let's write the code now. What will be sent in the email? Let's say we want to send a welcome mail when users sign up.
Open devise-mailer