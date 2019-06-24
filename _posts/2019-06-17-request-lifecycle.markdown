---
layout: post
title:  "Rails Request Lifecycle..."
date:   2019-06-12
---

Have you ever wondered how a request is processed in its lifecycle? What happens with request at each stage? 
Who handles request at what level? Let's dig it out!

Blog in progress..

Breakdown of request flow -
1. Browser generates HTTP/HTTPS request after a click or a event
2. Web server receives request, analyses it and passes to application server
3. Application server calls up proper controller-action after talking with router
4. The resulted output is sent back to browser and displayed on screen



- Web Browser
<p> Browser should direct request to a specific destination. For users it is a URL seen on web page, but
 computers need IP addresses, they do not understand these URLs. For this, there is a system in place called 
 Domain Name System(DNS) which maps URLs to computer understandable IP addresses. It is browser then who
 starts finding out IP address. Generally Interner Service Providers(ISP) keeps this information. If not then
 it can go up the hierarchy till Root DNS --> Extension wise Name Servers --> Authoritative DNS Server. The
 chase ends here. We got required ip address. Moving to next step... 
</p>