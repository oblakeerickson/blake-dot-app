---
layout: post
title: "Validations"
date: 2013-03-22 01:00:00 -0600
---

I started learning web development with Sinatra, which so far has satisfied my needs and has gotten the job done, but I think I’m starting to experience it’s limitations.

I'm in the process of learning Rails and I learned how to apply validation to forms. If you don’t know what validation are, they are basically a way to ensure that the data in a form you are submitting meets certain criteria. For example in a registration form you have an email address, username, password, password confirmation etc. and you want to make sure that a user doesn’t sign up with a username that is already taken.

When I made my registration form for networkcraft.net I hacked together my own validation, but Rails or I guess Active Record makes validation much easier. Here is an example of what I’m talking about:

``` ruby
validates :content, :length => { :maximum => 140 }
```

This limits the content field of a form to 140 characters and if you do exceed the limit it will fire off a flash error message, which is way better than having to do this manually. I'm sure there is a way to do validations in Sinatra, but I feel like Rails was designed for this.

Here are a couple of other links about validations in Rails: [Active Record Validations Callbacks](https://web.archive.org/web/20130408093146/http://guides.rubyonrails.org/active_record_validations_callbacks.html) and [Validations in Rails 3](https://web.archive.org/web/20130408093146/http://railscasts.com/episodes/211-validations-in-rails-3).

