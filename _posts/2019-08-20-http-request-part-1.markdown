---
layout: post
title:  "Demystifying HTTP request - Part 1"
date:   2019-08-20
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails http https headers body response"
---

HTTP request headers can be broadly divided into 3 parts - 
1. General
2. Response Headers
3. Request Headers 

<br>
### General
<br>

`"GET /blog HTTP/1.1"`

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