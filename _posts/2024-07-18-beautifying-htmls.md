---
layout: post
title:  "HAML - Beautifying HTMLs"
date:   2024-07-18
keywords: "ruby rails github learning html haml markup_language ruby_on_rails"
image: assets/images/haml.png
categories: [ Rails, Markup, HTML ]
---

<br>

<h2>What?</h2>

HAML is HTML Abstract Markup Language. It is developed on one core principle - to beautify markup. But at the same time
it also helps in maintaining DRY, well intended and structured code. Haml markup is similar to CSS in syntax. For example, Haml has the same dot . representation for classes as CSS does. It is around from 2006 and is still actively maintained.

<br>

<h2>Why?</h2>

<strong> 1. Reduced repetition aka DRY</strong>

HTML involves lot of repetition - once at the start and at the end of actual content. ERB also adds some repetition.<br>
For example:

```html
<p>Example Paragraph</p>
```

HAML reduces this repetition like -

```haml
%p Example Paragraph
```

To make this work HAML relies on indentation.

<strong>2. Indented & structured code</strong>

HAML forces use of strict indentation. The direct benefit of it is more structured code. For example look at this code.
The mixture of these qualities make the code beautiful. However defining beautiful code is hard, but as mentioned in HAML documentation it is one of their core principle.

<strong>3. Executes ruby code</strong>

It's also possible to embed Ruby code into Haml documents. An equals sign, =, 
will output the result of the code. A hyphen, -, will run the code but not output 
the result. It also supports control statements like if, while.

<br>

<h2>How?</h2>

To get more out of this article, let's convert a HTML code block into HAML code.

Example 1:

HTML -

```html
<section class="container">
  <h1><%= post.title %></h1>
  <h2><%= post.subtitle %></h2>
  <div class="content">
    <%= post.content %>
  </div>
</section>
```

HAML -

```haml
%section.container
  %h1= post.title
  %h2= post.subtitle
  .content
    = post.content
```

Example 2:

HTML -

```html
<nav class="navbar">
  <ul class="nav-list">
    <li class="nav-item">
      <a href="/">Home</a>
    </li>
    <li class="nav-item">
      <a href="/about">About</a>
    </li>
    <li class="nav-item">
      <a href="/services">Services</a>
    </li>
    <li class="nav-item">
      <a href="/contact">Contact</a>
    </li>
  </ul>
</nav>

<section class="hero">
  <h1>Welcome to Our Website</h1>
  <p>We provide amazing services to our clients.</p>
</section>

<section class="about">
  <h2>About Us</h2>
  <p>We are a company dedicated to providing the best services in the industry.</p>
</section>

<section class="services">
  <h2>Our Services</h2>
  <ul class="service-list">
    <li class="service-item">Consulting</li>
    <li class="service-item">Development</li>
    <li class="service-item">Support</li>
  </ul>
</section>
```

<br>
HAML -

```haml
%nav.navbar
  %ul.nav-list
    %li.nav-item
      %a{ href: "/" } Home
    %li.nav-item
      %a{ href: "/about" } About
    %li.nav-item
      %a{ href: "/services" } Services
    %li.nav-item
      %a{ href: "/contact" } Contact

%section.hero
  %h1 Welcome to Our Website
  %p We provide amazing services to our clients.

%section.about
  %h2 About Us
  %p We are a company dedicated to providing the best services in the industry.

%section.services
  %h2 Our Services
  %ul.service-list
    %li.service-item Consulting
    %li.service-item Development
    %li.service-item Support

```

Did you noticed the change? I know it is hard to miss. Imagine the impact it can have on large codebase. It can
make them more maintainable and readable. Also its latest release supports ruby version >= 2.1.0


References -
1. https://haml.info
2. https://github.com/haml/haml
