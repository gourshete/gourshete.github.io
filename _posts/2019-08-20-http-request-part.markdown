---
layout: post
title:  "HTTP request response headers"
date:   2019-08-20
categories: [ Rails ]
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response general"
---

At the end browser talks in the language of HTTP request. But we really know minimal about it. 

The request process flow is as simple as browser sends http request to the server and receives a response. Sometimes what we see is a combined result of 
responses from multiple requests.

To summarize every image, text or anything seen on browser is a response received to an http request. 

Let's see what a request and response headers of http request consists of.
 
HTTP request headers can be broadly divided into 3 parts - 
1. General
2. Response Headers
3. Request Headers 

<br>
### General
<br>

Sample HTTP request format <br>`"GET /blog HTTP/1.1"`

Let's divide it into sections and see what each one means

- Method

`GET` is a method used in http request which indicates type of work expected from request. There are methods like `POST, DELETE, PUT, PATCH`.


- Path

It tells at what url should server look for. e.g.
`https://gryffindor.in/`


- Version

HTTP protocol version as 1.1 or 2.0

- Status Code

It is a 3 digit code that represents response from server. Like<br>
`Status Code: 304`

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
