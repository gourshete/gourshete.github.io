---
layout: post
title:  "APIs in Rails 5.0"
date:   2018-03-23
keywords: "API in rails 5. rails github gryffindor learning api"
---

Have you ever wonder how APIs work in the world of convention over configuration, specifically in Rails 5.0?

<img src="{{ '/assets/img/web_api.png' | prepend: site.baseurl }}" alt="">

Rails keeps continuing its legacy of convention over configuration in APIs also. Before Rails 5, we used to use rails-api to implement APIs. But now rails-api is merged to core Rails. So Rails 5 has in-built support for APIs. That’s great!!!

<h5>Web app or API app</h5>
In normal rails web app, there are two parts. One part retrieves data to be served, and other part renders that data into HTML, CSS to see a beautiful webpage. And to note, both the parts are done by Rails itself.

But in case of APIs, rails will only be responsible for retrieving data ( it will return data in JSON, XML, etc formats as output ) and the rendering will be performed by other framework like AngularJs, etc or it is just out of scope of rails.

<h5>What is different in API mode?</h5>

The major difference in API mode would be, to cut down the needed setup to a very minimal. It would not generate views, helpers and assets. Basically, API mode removes functionality that you do not need.

If you start building API server first Rails app, this will do three main things for you -

* Configure your application to start with a more limited set of middleware than normal. Specifically, it will not include any middleware primarily useful for browser applications (like cookies support) by default.

* Make ApplicationController inherit from ActionController::API instead of ActionController::Base. As with middleware, this will leave out any Action Controller modules that provide functionalities primarily used by browser applications.

* Configure the generators to skip generating views, helpers and assets when you generate a new resource.

That’s it! A short introduction on Rails APIs. Stay tuned for How to build an Rails API app.


<a href='https://medium.com/@swapnilggourshete/apis-in-rails-5-0-a3b3033b4ad' target='_blank'>Medium Blog</a>


