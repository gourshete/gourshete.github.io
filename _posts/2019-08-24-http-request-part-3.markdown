---
layout: post
title:  "Ruby HTTP request response - 3"
date:   2019-08-24
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response"
---


HTTP request headers can be broadly divided into 3 parts - 
1. General
2. Response Headers
3. Request Headers 

<br>
### Request Headers
<br>

Sample HTTP request format `"GET /blog HTTP/1.1"`

Let's divide it into sections and see what each one means

- Accept

Tells about response formats that client can accept. e.g.<br>
`text/html, application/json, application/xml, text/css, image/*, */*` 

- Referer

Allows client to specify from which URI this http request is generated/ requested. Like<br>
`Referer: https://buff.ly/`<br>
It is of great help for analytics.

- User agent

Indicates which browser the request is sent from. like<br>
`user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.100 Safari/537.36`


- Cache-control <br>
Used to indicate various flags in cache control mechanism. Like 
  1. max-age - to indicate client accepts cached data whose age is not greater than value in seconds).
  2. public - server can use any cache to store data
  3. no-cache - cache must not use data for subsequent request without re-validation.
  4. no-store - server can not use cache the request or response.
  5. must-revalidate - revalidate stale data before using

<br>
