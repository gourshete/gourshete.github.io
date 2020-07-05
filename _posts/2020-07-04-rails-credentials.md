---
layout: post
title:  "Rails - Managing secrets using credentials"
date:   2020-07-04
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails secrets kubernetes
postgres"
image: assets/images/grafana-dashboard.png
categories: [ Rails, Secret keys ]
---

How do you manage secret keys? We cannot commit them in Version Control System (like github), it is too dangerous.

In the era of docker-kubernetes we make them available as environment variables using kubernetes secrets & then application
code picks up from there. This way is okay but becomes lengthy when number of secrets keys goes up.

Let's talk about rails credentials now - the way for managing secret keys in the rails eco system itself. How different
this approach is? Well, it stores secret keys in application code itself, but those are encrypted and needs a master key to
decrypt. So, we can place just one secret key i.e. master key outside of VCS. Isn't it good?


- Create/edit credentials

```bash
EDITOR='VIM' rails credentials:edit
```

This will create two files `credentials.yml.enc` & `master.key` and open up decrypted credentials.yml.enc

```ruby
aws:
   access_key_id: 123
   secret_access_key: 345

# Used as the base secret for all MessageVerifiers in Rails, including the one protecting cookies.
secret_key_base:
```

Before saving these keys will be encrypted using master key. Note do not commit `master.key` file.

And these credentials can be accessed in rails environment as

```ruby
 > Rails.application.credentials.config
 => {:aws=>{:access_key_id=>123, :secret_access_key=>345}}
```

- The only key that would stored out of VCS is master key. There are multiple ways to achieve it. 


Thanks for reading.

...

  References - 
 
- [Blog](https://blog.saeloun.com/2019/10/10/rails-6-adds-support-for-multi-environment-credentials.html) on rails credentials
