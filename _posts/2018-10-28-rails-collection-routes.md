---
layout: post
title: "Rails Collection Routes"
date: 2018-10-28 01:00:00 -0600
---

While working on Pistachio, the todo app I'm building to practice rails, I
wanted to work on a new feature that would allow me to order lists. I already
had the ability to order items in a list but not the lists themselves. As I was
working on this feature I realized that maybe my original route for sorting
items wasn't actually the best route to be using especially since it would mean
that I would have two `sort` routes on my lists controller.

Here is what I originally had for sorting list items in my `config/routes.rb`
file:

```
resources :lists, only: [:index, :show, :new, :create, :destroy, :edit, :update] do
  patch :sort
end
```

which means the route looks like this `lists/:list_id/sort`.

This actually worked fine, but it was a bit weird that I had my sort item logic
inside of my lists controller. I'm sure I original did it this way because I
wasn't sure how to make a collection route that would hit my items controller
without requiring an item id, nor did I know it was called a collection route
that I was looking for.

Before we fix the lists route let's go ahead and create this collection based sort
route under the items resource:

```
resources :items, only: [:create, :destroy, :edit, :update] do
  patch :complete
  collection do
    patch :sort
  end
end
```

This will create a route for us that looks like `/lists/:list_id/items/sort`. Which then means I can move the contents of the current sort method in my lists controller to the sort method of my items controller where it should have been in the first place.

And now we can move the current `patch :sort` route that is part of the lists resources into a collection so that we can use it for sorting lists. It should now look like:

```
resources :lists, only: [:index, :show, :new, :create, :destroy, :edit, :update] do
  patch :sort
  collection do
    patch :sort
  end
end
```

This will give us a route of '/lists/sort` which is exactly what we want so that the sort route isn't tied to any specific route id, but instead to the whole collection of lists.
