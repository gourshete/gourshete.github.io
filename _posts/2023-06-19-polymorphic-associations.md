---
layout: post
title:  "Polymorphic Associations"
date:   2023-06-19
keywords: "ruby rails aws github learning swapnil gourshete ruby on rails"
image: assets/images/multiple-Inheritance-home-image.png
categories: [ Ruby, Rails]
---

<!--- Define -->
Suppose we have two models to which third model needs to be associated. It can be done with Polymorphic associations, Two or more models can be associated to third model using single association.


## How to use it?
There are two parts -
1. Migration defining two fields on the model which will have work as base model. It will have `association_id` -> `int` and `association_type` -> `string`.
2. Defining associations in models.

Lets understand through code example.


## Code Example
Suppose we have three models - Picture, User, Product

#### 1. Migration
We will add two fields `imageable_type` and `imageable_id`.
<img src="{{ '/assets/images/poly-1.png' | prepend: site.baseurl }}" alt="class-inheritance-example">

#### 2. Model associations changes
<img src="{{ '/assets/images/poly-2.png' | prepend: site.baseurl }}" alt="class-inheritance-example">




Extra Benefits
- From an instance of the Employee model, you can retrieve a collection of pictures: @employee.pictures
- Similarly, you can retrieve @product.pictures

Summarize


---

*In this post we will learn about multiple inheritance in ruby*.


**What is Multiple Inheritance?**

It is property of code to inherit from multiple parent classes. Ruby supports inheriting only from one parent class.

<img src="{{ '/assets/images/class-1.png' | prepend: site.baseurl }}" alt="class-inheritance-example">


So what is the way for inheriting from multiple classes? By the way are you aware of classic diamond problem in
mulitple inheritance? [If not, read more about it here.](https://en.wikipedia.org/wiki/Multiple_inheritance)

Here comes in play modules in Ruby. Modules are somewhat different than classes -
1. Modules can't be instantiated, class can be instantiated
2. Can't create object of Modules, but can create object of class
3. We can include multiple modules in a single class, but can't include classes


To achieve multiple inheritance, we can include as many modules in a class. The same methods will be overriden by latest implementation. Let's take a example -

<img src="{{ '/assets/images/class-modules-2.png' | prepend: site.baseurl }}" alt="class-inheritance-example">

Here module A is included in `class C` and so when method `name` is called upon `class C` it results printing `"A"`

Now let's consider this example - 

<img src="{{ '/assets/images/class-modules-3.png' | prepend: site.baseurl }}" alt="class-inheritance-example">

Here we have two modules `A` and `B`. And when these two are included in `class C`, because both define same method `name` and module `B` is included after A - the program output is `"B"`

And that's how we can include multiple modules in same class.

I hope this was useful!

---

<br>

  References - 
 
- [The Diamond problem](https://en.wikipedia.org/wiki/Multiple_inheritance)
