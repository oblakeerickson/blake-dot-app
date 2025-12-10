---
layout: post
title:  "Accepts Nested Attributes For"
date:   2014-01-22 01:00:00 -0600
---

Today I worked on adding a company name to my signup form. In order for me to get the form to work correctly I discovered that I needed the rails method `accepts_nested_attributes_for` in my company model:

```
class Company < ActiveRecord::Base
  has_many :users, dependent: :destroy
  validates :name, presence: true, length: { maximum: 75 }
  validates :plan, presence: true
  accepts_nested_attributes_for :users
end
```

And then inside your 'new action' inside of your companies controller you need to make sure a new user gets created as part of a company:

```
def new
  @company = Company.new
  @user = @company.users.build
end
```

Now finally we can work on our form. The first part of the form you do regularly and pass in `@company` into the `form_for` method. And then you notice that we have a `fields_for` section for the part of the form that has to deal with `users`.

```
<%= form_for(@company) do |f| %>
  <%= render 'shared/error_messages', object: f.object %>
  <%= f.label :company %>
  <%= f.text_field :name %>

  <%= f.fields_for :users do |user| %>

    <%= user.label :name %>
    <%= user.text_field :name %>

    <%= user.label :email %>
    <%= user.text_field :email %>

    <%= user.label :password %>
    <%= user.password_field :password %>

    <%= user.label :password_confirmation, "Confirmation" %>
    <%= user.password_field :password_confirmation %>

  <% end %>

  <%= f.submit "Create my account", class: "btn btn-large btn-primary" %>
```
And that's pretty much all you have to do in order to get a nested form to work.
