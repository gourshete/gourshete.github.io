---
layout: post
title:  "HTTP Status Codes: An Overview"
date:   2024-07-25
keywords: "ruby rails github learning http status codes ruby_on_rails"
image: assets/images/status_codes.jpg
categories: [ Rails]
---

<br>

HTTP status codes are an essential part of web communication, indicating the result of a client's request to a server. Here's an expanded list of status codes, their meanings, and how to use them in a Rails API.

---

### 1xx: Informational

#### 100
code - 100 <br>
status - `:continue` <br>
Info - Continue

```ruby
# This is typically handled by the server automatically
```

**---**

#### 101
code - 101 <br>
status - `:switching_protocols` <br>
Info - Switching Protocols

```ruby
# This is typically handled by the server automatically
```

**---**


#### 102
code - 102 <br>
status - `:processing` <br>
Info - Processing

```ruby
# This is typically used in WebDAV
```

---

## 2xx: Success

#### 200
code - 200 <br>
status - `:ok` <br>
Info - OK

```ruby
render json: { message: 'Success' }, status: :ok
```

**---**

#### 201
code - 201 <br>
status - `:created` <br>
Info - Created

```ruby
render json: { message: 'Resource created' }, status: :created
```

**---**

#### 202
code - 202 <br>
status - `:accepted` <br>
Info - Accepted

```ruby
render json: { message: 'Request accepted for processing' }, status: :accepted
```

**---**

#### 203
code - 203 <br>
status - `:non_authoritative_information` <br>
Info - Non-Authoritative Information

```ruby
render json: { message: 'Information from a third-party source' }, status: :non_authoritative_information
```

**---**

#### 204
code - 204 <br>
status - `:no_content` <br>
Info - No Content

```ruby
head :no_content
```

**---**

#### 205
code - 205 <br>
status - `:reset_content` <br>
Info - Reset Content

```ruby
head :reset_content
```

**---**

#### 206
code - 206 <br>
status - `:partial_content` <br>
Info - Partial Content

```ruby
render json: { partial_data: data }, status: :partial_content
```

---

## 3xx: Redirection

#### 300
code - 300 <br>
status - `:multiple_choices` <br>
Info - Multiple Choices

```ruby
render json: { choices: options }, status: :multiple_choices
```

**---**

#### 301
code - 301 <br>
status - `:moved_permanently` <br>
Info - Moved Permanently

```ruby
redirect_to new_url, status: :moved_permanently
```

**---**

#### 302
code - 302 <br>
status - `:found` <br>
Info - Found

```ruby
redirect_to other_url, status: :found
```

**---**

#### 303
code - 303 <br>
status - `:see_other` <br>
Info - See Other

```ruby
redirect_to other_url, status: :see_other
```

**---**

#### 304
code - 304 <br>
status - `:not_modified` <br>
Info - Not Modified

```ruby
head :not_modified
```

**---**

#### 307
code - 307 <br>
status - `:temporary_redirect` <br>
Info - Temporary Redirect

```ruby
redirect_to temp_url, status: :temporary_redirect
```

**---**

#### 308
code - 308 <br>
status - `:permanent_redirect` <br>
Info - Permanent Redirect

```ruby
redirect_to new_permanent_url, status: :permanent_redirect
```

---

## 4xx: Client Errors

#### 400
code - 400 <br>
status - `:bad_request` <br>
Info - Bad Request

```ruby
render json: { error: 'Invalid parameters' }, status: :bad_request
```

**---**

#### 401
code - 401 <br>
status - `:unauthorized` <br>
Info - Unauthorized

```ruby
render json: { error: 'Authentication required' }, status: :unauthorized
```

**---**

#### 402
code - 402 <br>
status - `:payment_required` <br>
Info - Payment Required

```ruby
render json: { error: 'Payment required to access this resource' }, status: :payment_required
```

**---**

#### 403
code - 403 <br>
status - `:forbidden` <br>
Info - Forbidden

```ruby
render json: { error: 'Access denied' }, status: :forbidden
```

**---**

#### 404
code - 404 <br>
status - `:not_found` <br>
Info - Not Found

```ruby
render json: { error: 'Resource not found' }, status: :not_found
```

**---**

#### 405
code - 405 <br>
status - `:method_not_allowed` <br>
Info - Method Not Allowed

```ruby
render json: { error: 'Method not allowed' }, status: :method_not_allowed
```

**---**

#### 406
code - 406 <br>
status - `:not_acceptable` <br>
Info - Not Acceptable

```ruby
render json: { error: 'Not acceptable' }, status: :not_acceptable
```

**---**

#### 409
code - 409 <br>
status - `:conflict` <br>
Info - Conflict

```ruby
render json: { error: 'Resource conflict' }, status: :conflict
```

**---**

#### 410
code - 410 <br>
status - `:gone` <br>
Info - Gone

```ruby
render json: { error: 'Resource no longer available' }, status: :gone
```

**---**

#### 422
code - 422 <br>
status - `:unprocessable_entity` <br>
Info - Unprocessable Entity

```ruby
render json: { errors: resource.errors }, status: :unprocessable_entity
```

**---**

#### 429
code - 429 <br>
status - `:too_many_requests` <br>
Info - Too Many Requests

```ruby
render json: { error: 'Rate limit exceeded' }, status: :too_many_requests
```

---

## 5xx: Server Errors

#### 500
code - 500 <br>
status - `:internal_server_error` <br>
Info - Internal Server Error

```ruby
render json: { error: 'Internal Server Error' }, status: :internal_server_error
```

**---**

#### 501
code - 501 <br>
status - `:not_implemented` <br>
Info - Not Implemented

```ruby
render json: { error: 'Functionality not implemented' }, status: :not_implemented
```

**---**

#### 502
code - 502 <br>
status - `:bad_gateway` <br>
Info - Bad Gateway

```ruby
render json: { error: 'Bad Gateway' }, status: :bad_gateway
```

**---**

#### 503
code - 503 <br>
status - `:service_unavailable` <br>
Info - Service Unavailable

```ruby
render json: { error: 'Service Unavailable' }, status: :service_unavailable
```

**---**

#### 504
code - 504 <br>
status - `:gateway_timeout` <br>
Info - Gateway Timeout

```ruby
render json: { error: 'Gateway Timeout' }, status: :gateway_timeout
```

**---**

#### 507
code - 507 <br>
status - `:insufficient_storage` <br>
Info - Insufficient Storage

```ruby
render json: { error: 'Insufficient storage' }, status: :insufficient_storage
```

**---**

#### 511
code - 511 <br>
status - `:network_authentication_required` <br>
Info - Network Authentication Required

```ruby
render json: { error: 'Network authentication required' }, status: :network_authentication_required
```

---

Note that while Rails provides symbols for many status codes, you can always use the numerical code directly if a symbol is not available:

```ruby
render json: { message: 'Custom status' }, status: 418
```

When building APIs, using appropriate status codes helps clients understand and handle responses correctly, leading to more robust and maintainable applications. It's important to choose the most specific and appropriate status code for each situation to provide clear and accurate information to API consumers.