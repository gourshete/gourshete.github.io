---
layout: post
title:  "Rails Request Lifecycle..."
date:   2019-06-12
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
<p> Browser should direct request to a specific destination. For users it is a URL seen on web page, but
 computers need IP addresses, they do not understand these URLs.</p> 
<p>For this purpose, there is a system in place called 
 Domain Name System(DNS) which maps URLs to computer understandable IP addresses. It is browser then who
 starts finding out IP address.</p> 
 <p>Generally Internet Service Providers(ISP) keeps this information. If not then
 it can go up the hierarchy LIKE Root DNS --> Extension wise Name Servers --> Authoritative DNS Server. The
 chase ends here. We got required ip address. </p>
 
<p>
 <img src="{{ '/assets/img/dig.png' | prepend: site.baseurl }}" alt="">
 Moving to next step... 
</p>

<p>..</p>

<h3> Web Server </h3>

<p>By now browser is successfully connected to server. The server here is web server. Some examples are Apache,
Nginx, Passenger, Puma, Unicorn, Webrick.</p> 
<p>These servers are meant to talk only in http. Their job is to understand the request and make decision on how to sevice
 that request.</p>
<p>For simpler request, we can configure web server easily. Suppose we need to tell web server that if browser asks for any 
assets then serve it from '/public/assets' folder. There are a list of different web servers you can use for this purpose.
 With nginx it is like 
</p>
<p>
<script src="https://gist.github.com/SGourshete/8c459576dc82eb38c62deb826e4ae20d.js"></script>
</p>
<p>Okay then. We are set to serve requests for assets. If browser asks for assets it will receive an expected response in output,
for anything else than assets, it will get 404 not found response.</p>
<p>But what if browser asks for latest 10 blog posts from xyz author with some amazing styling and javascript??</p>
<p> Our current configuration does not support this kind of request. Even if we decide to handle it at this level, it will be 
complex to put it in web server configuration file. So what next?</p>
<p>There comes Rails! Web server passes request to Rails application. But there can be many ways for web server to do it.
 Just to understand, it can call a method with argument or declare variables or use global variables. Even if we managed
 this, another question arises, in what format should Rails sends data back to web server? To reduce this confusion,
 there is a system in place called RACK</p>
