---
layout: post
title:  "Demystifying http request"
date:   2019-08-22
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response"
---

`"GET /blog HTTP/1.1"`

- Method

`GET` is a method used in http request which indicates type of work expected from request. There are methods like `POST, DELETE, PUT, PATCH`.


- Path

It tells at what url should server look for. e.g.
`https://gryffindor.in/`


- Version

HTT(P-protocol) version as 1.1 or 2.0

- Cache-control <br>
Used to indicate various flags in cache control mechanism. Like 
  1. max-age - to indicate client accepts cached data whose age is not greater than value in seconds).
  2. public - server can use any cache to store data
  3. no-cache - cache must not use data for subsequent request without re-validation.
  4. no-store - server can not use cache the request or response.
  5. must-revalidate - revalidate stale data before using

<br>
- Date

All http requests use Greenwich Standard Time(GMT) or UTC. Here is common format -<br> 
'Date: Fri, 23 Aug 2019 10:17:27 GMT'<br>
reference - [RFC](http://tools.ietf.org/html/rfc7231#section-7.1.1.1)

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