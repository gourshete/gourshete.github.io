---
layout: post
title:  "Ruby HTTP request response - 1"
date:   2019-08-20
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response"
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
