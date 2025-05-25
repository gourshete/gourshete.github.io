---
layout: post
title:  "HTTP Status Codes: An Overview"
date:   2024-07-25
keywords: "ruby rails http status codes ruby_on_rails example"
image: assets/images/status_codes.jpeg
categories: [ Rails]
---

<br>

HTTP status codes are an essential part of web communication, indicating the result of a client's request to a server. Here's an expanded list of status codes, their meanings, and how to use them in a Rails API.

---

# ✅ HTTP Status Code Cheat Sheet

<br>

<table border="1">
  <thead>
    <tr>
      <th style="padding-left: 10px;">Category</th>
      <th style="padding-left: 10px;">Code</th>
      <th style="padding-left: 10px;">Symbol</th>
      <th style="padding-left: 10px;">Meaning</th>
      <th style="padding-left: 10px;">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding-left: 10px;">1xx – Informational</td>
      <td style="padding-left: 10px;">100</td>
      <td style="padding-left: 10px;">:continue</td>
      <td style="padding-left: 10px;">Continue</td>
      <td style="padding-left: 10px;">Request received, continue processing</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">1xx – Informational</td>
      <td style="padding-left: 10px;">101</td>
      <td style="padding-left: 10px;">:switching_protocols</td>
      <td style="padding-left: 10px;">Switching Protocols</td>
      <td style="padding-left: 10px;">Protocol switch accepted</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">2xx – Success</td>
      <td style="padding-left: 10px;">200</td>
      <td style="padding-left: 10px;">:ok</td>
      <td style="padding-left: 10px;">OK</td>
      <td style="padding-left: 10px;">Request succeeded</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">2xx – Success</td>
      <td style="padding-left: 10px;">201</td>
      <td style="padding-left: 10px;">:created</td>
      <td style="padding-left: 10px;">Created</td>
      <td style="padding-left: 10px;">Resource created successfully</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">2xx – Success</td>
      <td style="padding-left: 10px;">204</td>
      <td style="padding-left: 10px;">:no_content</td>
      <td style="padding-left: 10px;">No Content</td>
      <td style="padding-left: 10px;">Success, no content returned</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">3xx – Redirection</td>
      <td style="padding-left: 10px;">301</td>
      <td style="padding-left: 10px;">:moved_permanently</td>
      <td style="padding-left: 10px;">Moved Permanently</td>
      <td style="padding-left: 10px;">Resource moved to a new URI</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">3xx – Redirection</td>
      <td style="padding-left: 10px;">302</td>
      <td style="padding-left: 10px;">:found</td>
      <td style="padding-left: 10px;">Found</td>
      <td style="padding-left: 10px;">Resource temporarily moved</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">3xx – Redirection</td>
      <td style="padding-left: 10px;">304</td>
      <td style="padding-left: 10px;">:not_modified</td>
      <td style="padding-left: 10px;">Not Modified</td>
      <td style="padding-left: 10px;">Use cached version</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">400</td>
      <td style="padding-left: 10px;">:bad_request</td>
      <td style="padding-left: 10px;">Bad Request</td>
      <td style="padding-left: 10px;">Malformed request syntax</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">401</td>
      <td style="padding-left: 10px;">:unauthorized</td>
      <td style="padding-left: 10px;">Unauthorized</td>
      <td style="padding-left: 10px;">Auth required</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">403</td>
      <td style="padding-left: 10px;">:forbidden</td>
      <td style="padding-left: 10px;">Forbidden</td>
      <td style="padding-left: 10px;">Access denied</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">404</td>
      <td style="padding-left: 10px;">:not_found</td>
      <td style="padding-left: 10px;">Not Found</td>
      <td style="padding-left: 10px;">Resource not found</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">405</td>
      <td style="padding-left: 10px;">:method_not_allowed</td>
      <td style="padding-left: 10px;">Method Not Allowed</td>
      <td style="padding-left: 10px;">HTTP method not supported</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">4xx – Client Error</td>
      <td style="padding-left: 10px;">422</td>
      <td style="padding-left: 10px;">:unprocessable_entity</td>
      <td style="padding-left: 10px;">Unprocessable Entity</td>
      <td style="padding-left: 10px;">Validation errors</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">5xx – Server Error</td>
      <td style="padding-left: 10px;">500</td>
      <td style="padding-left: 10px;">:internal_server_error</td>
      <td style="padding-left: 10px;">Internal Server Error</td>
      <td style="padding-left: 10px;">Generic server error</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">5xx – Server Error</td>
      <td style="padding-left: 10px;">502</td>
      <td style="padding-left: 10px;">(no symbol)</td>
      <td style="padding-left: 10px;">Bad Gateway</td>
      <td style="padding-left: 10px;">Invalid upstream response</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">5xx – Server Error</td>
      <td style="padding-left: 10px;">503</td>
      <td style="padding-left: 10px;">:service_unavailable</td>
      <td style="padding-left: 10px;">Service Unavailable</td>
      <td style="padding-left: 10px;">Server temporarily overloaded</td>
    </tr>
    <tr>
      <td style="padding-left: 10px;">5xx – Server Error</td>
      <td style="padding-left: 10px;">504</td>
      <td style="padding-left: 10px;">(no symbol)</td>
      <td style="padding-left: 10px;">Gateway Timeout</td>
      <td style="padding-left: 10px;">Upstream timeout</td>
    </tr>
  </tbody>
</table>

<br>
<br>

ℹ️ For the full list of symbols supported by Rails, visit the [Rails Response Status Documentation](https://api.rubyonrails.org/classes/ActionDispatch/Response.html#method-c-status_code).