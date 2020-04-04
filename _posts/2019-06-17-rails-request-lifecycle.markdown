---
layout: post
title:  "Rails Request Lifecycle..."
date:   2019-06-12
comments: true
keywords: "Request lifecycle. How request passes through each stage. From Browser to Web server to Application server to
controller's action and back to browser. rails github gryffindor learning request lifecycle http browser webserver application server
nginx routes controller action rack app"
image: assets/images/dig.png
categories: [ Rails ]
tags: 'featured'
---

Have you ever wondered how a request is processed in its lifecycle? What happens with request at each stage? 
Who handles request at what level? Let's dig it out!

Breakdown of request flow -
1. Browser generates HTTP/HTTPS request after a click or a event
2. Web server receives request, analyses it and passes to application server
3. Application server calls up proper controller-action after talking with router
4. The resulted output is sent back to browser and displayed on screen

<p>.</p>

<h3>  Web Browser </h3>
Browser should direct request to a specific destination. For users it is a URL seen on web page, but
 computers need IP addresses, they do not understand these URLs.
 
For this purpose, there is a system in place called Domain Name System(DNS) which maps URLs to computer
 understandable IP addresses. It is browser who starts finding out IP address.
  
Search begins from local cache, of both browser and computer. If local cache does not have IP address of requested site, 
 browser generally asks Internet Service Providers(ISP). If not found then
 it goes up the hierarchy LIKE Root DNS --> Extension wise Name Servers(like .com, .net, .org) --> And then to Authoritative DNS Server. The
 chase ends here.
  
Yay! We get the required ip address.

Authoritative DNS Server must have IP address for requested site, if not there are high chances that your domain name
 provider has not set up your domain information properly.
 
 It is actually interesting to try on terminal with dig,
 <img src="{{ '/assets/images/dig.png' | prepend: site.baseurl }}" alt="">

<p>..</p>

<h3> Web Server </h3>

By now browser is successfully connected to server. The server here is web server. Some examples are Apache,
Nginx, Passenger, Puma, Unicorn, Webrick. 
These servers are meant to talk only in http. Their job is to understand the request and make decision on how to sevice
 that request.
 
For simpler request, we can configure web server easily. Suppose we need to tell web server that if browser asks for any 
assets then serve it from '/public/assets' folder. There are a list of different web servers you can use for this purpose.
 With nginx it is like <script src="https://gist.github.com/gourshete/8c459576dc82eb38c62deb826e4ae20d.js"></script>

Okay then. We are set to serve requests for assets. If browser asks for assets it will receive an expected response in output,
for anything else than assets, it will get 404 not found response.

But what if browser asks for latest 10 blog posts from xyz author with some amazing styling and javascript??

Our current configuration does not support this kind of request. Even if we decide to handle it at this level, it will be 
complex to put it in web server configuration file. So what next?

There comes Rails! Web server passes request to Rails application. But there can be many ways for web server to do it.
 Just to understand, it can call a method with argument or declare variables or use global variables. Even if we managed
 this, another question arises, in what format should Rails sends data back to web server? To reduce this confusion,
 there is a system in place called RACK

<p>...</p>

<h4>RACK App</h4>
 
Rack is a simple Ruby protocol/convention that does a few things. The web server needs to tell the web framework,
 "Hey, here a request for you to handle. By the way, here are the deets for the request: paths, http verb, headers, etc." 
 On the other hand, the framework needs to tell the server, "Hey, that’s cool, I’ve handled it. Here is the result... the status
  code, headers, and body."
  
In order to remain lightweight and framework agnostic, Rack picked the simplest possible way to do this in Ruby. 
It notifies the web framework using a method call, communicates the details as method arguments, and the web framework 
communicates back by return values from the method call.

In code it just looks like
<script src="https://gist.github.com/gourshete/0a7a99300868b49c62ac87c895b923bc.js"></script>

Web server creates env hash to pass it to Rack's call method. This env hash has information like http_verb, 
 http_method, parameters, rack_app_version, etc.

And the call method responds in three variables - status, header and body. Status is http status, to tell about request completed
successfully or whatever happened with it. Headers is a hash of http headers, and Body is an array of response.


Coming to rails, the config.ru file will look something like 
<script src="https://gist.github.com/gourshete/e424bec8a866824af57377bfff2d4807.js"></script>

It is supposed to pass Rack application to run keyword, this means Rails.application is a Rack app and must respond to call method.

<p>....</p>

<h4>Our app</h4>

Finally request reaches our app. It is evaluated by again a Rack app generated by Rails using routes.rb!!! Yes that's 
too muck Rack apps around. But Rails is always been that.

config/routes.rb - 
<script src="https://gist.github.com/gourshete/2492f1ff1731060f206701583f279c5b.js"></script>

This will ultimately generate these seven routes
<script src="https://gist.github.com/gourshete/6909e997f7d11ed2b9ddb4b046d50c58.js"></script>

From here, most of us know how it works. 

If request is for `'/books'` and is of kind GET, it will go to `BooksController#index` action. Request GET for `'/books/:id'` will go 
to `BooksController#show` and likewise!

That's it from the Rails Request Lifecycle.

>Cheers!!! 

{% if page.comments %}
  <div id="disqus_thread"></div>
  <script>
    var disqus_config = function () {
      this.page.url = 'https://gryffindor.in/blog/2019/06/12/rails-request-lifecycle';
      this.page.identifier = 'rails-request-lifecycle';
    };
  
    (function() {
      var d = document, s = d.createElement('script');
      s.src = 'https://gryffindor-1.disqus.com/embed.js';
      s.setAttribute('data-timestamp', +new Date());
      (d.head || d.body).appendChild(s);
    })();
  </script>
  <noscript>
    Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a>
  </noscript>
{% endif %}