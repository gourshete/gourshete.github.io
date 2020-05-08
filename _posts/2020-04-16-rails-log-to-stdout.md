---
layout: post
title:  "Error in logging! Rails log to STDOUT"
date:   2020-03-27
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails logs log file stdout terminal"
image: assets/images/log.png
categories: [ Rails, Short Blog ]
---

Logs play important role in debugging application. Rails comes with six levels of logging :debug, :info, :warn, :error, :fatal,
 and :unknown. These logs are generally written to `Rails.root/logs/#{environment}.log` file of each environment. 
 
The point here is Rails new versions ships with settings to write logs to STDOUT and not environment specific log files. A
new environment variable named `RAILS_LOG_TO_STDOUT` is used to take the decision. In new rails app you will find following
code snippet in `production.rb`

```ruby
  if ENV['RAILS_LOG_TO_STDOUT'].present?
    logger           = ActiveSupport::Logger.new(STDOUT)
    logger.formatter = config.log_formatter
    config.logger    = ActiveSupport::TaggedLogging.new(logger)
  end
```

It tells the rails app to write logs to STDOUT and not to `Rails.root/log/production.log` if ENV['RAILS_LOG_TO_STDOUT'] is set to true.
The same setting is applied to all environments. This setting can be toggled by simply altering the value set to
 `ENV['RAILS_LOG_TO_STDOUT']`.


...
 
 * References - 
 
[Rails guide](https://guides.rubyonrails.org/debugging_rails_applications.html) - [https://guides.rubyonrails.org/debugging_rails_applications.html](https://guides.rubyonrails.org/debugging_rails_applications.html)