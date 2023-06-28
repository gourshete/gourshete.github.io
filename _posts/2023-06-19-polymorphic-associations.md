---
layout: post
title:  "Polymorphic Associations in Rails"
date:   2023-06-19
keywords: "ruby rails github learning ruby_on_rails polymorphic association activerecord"
image: assets/images/poly-main.png
categories: [ Ruby, Rails, Activerecord]
---

<!--- Define -->
Suppose two models can be associated to a third model with a common attribute. For example, `Image` can belong to `User` as well as `Product`, because user will have self image and product will have descriptive images of product.
This can be achieved with Polymorphic associations, Two or more models can be associated to third model using single association.


## How to use it?
There are two parts -
1. Migration defining two fields on the model which will have work as base model. It will have `association_id` -> `int` and `association_type` -> `string`.
2. Defining associations in models.

And we are ready to use it.

Lets understand through code example.


## Code Example
Suppose we have three models - Picture, User, Product. We need specify polymorphic association at
`pictures` table creation

#### 1. Migration
We will add two fields `imageable_type` and `imageable_id`.
<img src="{{ '/assets/images/poly-1.png' | prepend: site.baseurl }}" alt="class-inheritance-example">


#### 2. Model associations changes
<img src="{{ '/assets/images/poly-2.png' | prepend: site.baseurl }}" alt="class-inheritance-example">



### Benefits
The setup provides easy access to associated models.
- From an instance of the User model, you can retrieve a collection of pictures: `@user.pictures`
- Similarly, you can retrieve `@product.pictures`
- If you have an instance of the Picture model, you can get to its parent via `@picture.imageable`
- Polymorphic association helps in making your code DRY(Do not Repeat Yourself)



## Can we test polymorphic associations?
Yes, of course. I am using `rspec` for unit testing instead of `minitest`. It can be installed from here
<a href="https://github.com/rspec/rspec-rails" target="_blank">install rails rspec</a>.

If you had not installed rspec previously, run

```bash
$ rails generate rspec:model user
      create  spec/models/user_spec.rb

$ rails generate rspec:model product
      create  spec/models/product_spec.rb

$ rails generate rspec:model picture
      create  spec/models/picture_spec.rb
```

Now we have empty rspec files for models. Let's add following code to picture model rspec file
<img src="{{ '/assets/images/poly-rspec.png' | prepend: site.baseurl }}" alt="polymorphic-rspec-example">

And when we run this spec file
<img src="{{ '/assets/images/poly-run-rspec.png' | prepend: site.baseurl }}" alt="polymorphic-rspec-example">

It will pass with flying colors!

---

<br>

  References - 
 
- [Rails documentation](https://guides.rubyonrails.org/association_basics.html#polymorphic-associations)
- [rspec-rails](https://github.com/rspec/rspec-rails).