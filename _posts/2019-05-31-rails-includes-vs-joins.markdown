---
layout: post
title:  "Rails Includes vs Joins"
date:   2019-05-31
---

When I started learning Rails, I was always in a state of confusion about using includes or joins,
because both are used in almost same scenario. Includes uses eager loading whereas joins uses lazy 
loading. Both are used when certain operations are meant to be performed on associated tables. And 
here comes the difference.


<h4>What is the problem with Joins?</h4>

<img src="{{ '/assets/img/joins_all.png' | prepend: site.baseurl }}" alt="">

Here, we retrieved users in the first line and data is formatted in the each do loop. Here is interesting thing, to retrieve user.company.name, each time a call to database is made. It means, if there are 10k users then 10k separate queries would be fired up.
And this will overkill system when scaled up. Isn't there is efficient way? Yes, it is Includes.

And this will overkill system when scaled up. Isn't there a more efficient way? Yes, it is Includes.

<h3>INCLUDES</h3>
If we go through Rails documenting, it clearly says - 'With includes, Active Record ensures that all of the
specified associations are loaded using the minimum possible number of queries'. When we need data to be used
from associated tables, includes must be used.

Here is an example,

<img src="{{ '/assets/img/includes.png' | prepend: site.baseurl }}" alt="">

Here, the data from table companies is brought right in the first line, since it says includes companies.
No additional query is fired from the do loop for 'user.company.name'. Size of users table does not matter now.
It is scalable to any size.

Isn't it fantastic? Yes, it is. It saves hell lot of time. And it proves to be very efficient, when application
contains huge data.

- So, does includes always preferred over joins?

Hopefully not, there are some cases when includes does not exceed joins in terms of efficiency.

<img src="{{ '/assets/img/includes_3.png' | prepend: site.baseurl }}" alt="">
Here, we used tables users and companies, but companies is only for some sort of filter. We did not actually 
used data from companies later in the code. So no need to bring data from companies along with users. This is
 why join is efficient in this case.
 
Cheers!!!