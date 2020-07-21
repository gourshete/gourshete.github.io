---
layout: post
title:  "Rails 6 - Managing API keys using 'credentials'"
date:   2020-07-04
keywords: "ruby rails github gryffindor learning swapnil gourshete ruby on rails secrets kubernetes
postgres"
image: assets/images/lock5.png
categories: [ Rails, API keys, Secrets ]
---

How do you manage application secret keys? We cannot commit them in Version Control System (like github), it is too dangerous.

In the era of docker-kubernetes we make them available as environment variables using kubernetes secrets & then application
code picks up from there. This way is okay but becomes lengthy when number of secrets keys goes up.

Let's talk about rails credentials now - the way for managing secret keys in the rails eco system itself. How different
this approach is? Well, it stores secret keys in application code itself, but those are encrypted and needs a master key to
decrypt. So, we can place just one secret key i.e. master key outside of VCS. Isn't it good?


- Create/edit credentials

```bash
EDITOR='VIM' rails credentials:edit
```

This will create two files `credentials.yml.enc` & `master.key` and open up decrypted `credentials.yml.enc`

```ruby
aws:
   access_key_id: AWSACCESSKEYID
   secret_access_key: AWSSECRETACCESSKEY

# Used as the base secret for all MessageVerifiers in Rails, including the one protecting cookies.
secret_key_base:
```

This file will be encrypted again before saving. Note do not commit `master.key` file. The only key that would stored 
out of VCS is master key. There are multiple ways to achieve it.

- Accessing these in rails environment as

```ruby
 > Rails.application.credentials.config
 => {:aws=>{:access_key_id=>AWSACCESSKEYID, :secret_access_key=>AWSSECRETACCESSKEY}}
``` 

<br><br>

### Adding Environment wise Credentials

We can also keep dev, staging & production env wise separate credential files. Let's create it for development environment as -

```ruby
> rails credentials:edit --environment development
```

It will open up in a default editor like

```ruby
aws:
   access_key_id: 123
   secret_access_key: 456
```

Put in secrets in here & then can be simply accessed in application as

```ruby
 > Rails.application.credentials.config
 => {:aws=>{:access_key_id=>"DEVELOPMENT_KEY", :secret_access_key=>"DEVELOPMENT_ACCESS_KEY"}}
```

<br>
- The best thing I liked was this

<img src="{{ '/assets/images/development-credentials.png' | prepend: site.baseurl }}" alt="">

Even if you forget to remove secrets `key file` it will no be added to VCS as rails has moved it to `gitignore`.

Thanks for reading.

---

  References - 
 
- Saeloun [Blog](https://blog.saeloun.com/2019/10/10/rails-6-adds-support-for-multi-environment-credentials.html) on rails credentials

- Medium [Blog](https://medium.com/@kirill_shevch/encrypted-secrets-credentials-in-rails-6-rails-5-1-5-2-f470accd62fc) on environment wise credentials