---
layout: post
title:  "Resolve early termination of worker in Rails"
date:   2022-12-12
keywords: "ruby rails aws load-balancer ec2 instance github learning swapnil gourshete ruby on rails"
image: assets/images/stale-postmaster-pid-error.png
categories: [ Rails, Puma, Postgres ]
---

*In this post we will resolve the error - Early termination of puma worker*.

Note - The reason described below is one of the cause, it is quite possible to reproduce this issue due to another reason. 

Let's begin.

Few days ago, like every normal day I started dev environment rails server and suddenly server log flooded
with error message - `early-termination-of-worker`.

I did not understand at the time why it has happened as I did nothing different. Oh, but there was one thing to note - 
I had to abruptly shut down mac the day before. Was it even related?

**Yes, it was!**

While shutting down mac, postgres server was also abruptly closed - leading to `stale postmaster.pid` file in the
system. And the other day when I was trying to start rails server, it was unable to connect to postgres server. The 
reason was postgres server was unable to start as system had `stale postmaster.pid` reference.

If you are stuck at how I find out the reason, here it is - 

<img src="{{ '/assets/images/stale-postmaster-pid-error.png' | prepend: site.baseurl }}" alt="postgres-stale-postmaster-pid-error">

So after knowing the problem, answer was straight forward - **Go and delete postmaster.pid file**.

*How to do it?*

I use postgres desktop application, so these were steps for me -

1. Open terminal & navigate to Postgres directory. You can find postgres directory by opening postgres app and clicking 
on server settings option. My path was - <br> `/Users/swapnil/Library/Application Support/Postgres/var-13`

2. List all files in the directory and check if postmaster.pid file is present.
```ruby
ls -a
```
3. Go ahead and remove postmaster.pid -
```ruby
rm postmaster.pid
```

.

That's it. After this step your postgres server should be running & so rails server will be able to connect to it.

P.S. - If you installed postgres via different method then solution steps would be different for you.

---

Thanks. Cheers!


