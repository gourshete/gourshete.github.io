---
layout: post
title:  "Ruby HTTP request response - 2"
date:   2019-08-22
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response"
---
HTTP request headers can be broadly divided into 3 parts - 
1. General
2. Response Headers
3. Request Headers 

<br>
### Response Headers
<br>

Sample HTTP request format `"GET /blog HTTP/1.1"`

Let's divide it into sections and see what each one means


- date

All http requests use Greenwich Standard Time(GMT) or UTC. Here is common format -<br> 
'Date: Fri, 23 Aug 2019 10:17:27 GMT'<br>
reference - [RFC](http://tools.ietf.org/html/rfc7231#section-7.1.1.1)

- status

It is a 3 digit code that represents response from server. Like<br>
`Status Code: 304`

- expires

Tell the date when cookie will expire.

- last-modified

Tells date and time when origin of content was last modified.

- server

Tells the web server used to process this http request.

- cache-control <br>
Used to indicate various flags in cache control mechanism. Like 
  1. max-age - to indicate client accepts cached data whose age is not greater than value in seconds).
  2. public - server can use any cache to store data
  3. no-cache - cache must not use data for subsequent request without re-validation.
  4. no-store - server can not use cache the request or response.
  5. must-revalidate - revalidate stale data before using

<br>
