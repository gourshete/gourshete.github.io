---
layout: post
title:  "HAML - Beautifying HTMLs"
date:   2024-07-18
keywords: "ruby rails github learning html haml markup_language ruby_on_rails"
image: assets/images/haml.png
categories: [ Rails, Markup ]
---

Beautifying HTMLs using HAML

<br>

<h2>What?</h2>

HAML is HTML Abstract Markup Language. It is developed on one core principle - to beautify markup. But at the same time
it also helps in maintaining DRY, well intended and structured code. Haml markup is similar to CSS in syntax. For example, Haml has the same dot . representation for classes as CSS does. It is around from 2006 and is still actively maintained.

<br>

<h2>Why?</h2>

1. Reduced repetition aka DRY
HTML involves lot of repetition - once at the start and at the end of actual content. ERB also adds some repetition.<br>
For example <p>Example Paragraph</p>
HAML reduces this repetition like - %p Example Paragraph. 
To make this work HAML relies on indentation.

2. Indented & structured code
HAML forces use of strict indentation. The direct benefit of it is more structured code. For example look at this code.
The mixture of these qualities make the code beautiful. However defining beautiful code is hard, but as mentioned in HAML documentation it is one of their core principle.

3. Executes ruby code
It's also possible to embed Ruby code into Haml documents. An equals sign, =, 
will output the result of the code. A hyphen, -, will run the code but not output 
the result. It also supports control statements like if, while.

<br>

<h2>How?</h2>

To get more out of this article, let's convert a HTML code blog into HAML code.

```html
<section class="container">
  <h1><%= post.title %></h1>
  <h2><%= post.subtitle %></h2>
  <div class="content">
    <%= post.content %>
  </div>
</section>
```

```haml
%section.container
  %h1= post.title
  %h2= post.subtitle
  .content
    = post.content
```

Did you noticed the change? I know it is hard to miss. Imagine the impact it can have on large codebase. It can
make them more maintainable and readable. Also its latest release supports ruby version >= 2.1.0


References -
1. https://haml.info
2. https://github.com/haml/haml
