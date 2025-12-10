---
layout: post
title:  "Subdomain Constraints"
date:   2014-02-10 01:00:00 -0600
---

I've been reading through the Multi-Tenancy Rails book and today I studied the section on adding a subdomain constraint and just thought I would expand upon it today because I'm sure I'll need to use them again soon.

Basically a subdomain constraint will limit some routes to use a subdomain and other routes to use the normal domain routes. These constrained routes will be using separate controllerswhich is why we need thes special constraints.

Here is an example of what a constraint looks liks inside of your config/routes.rb file:

```
constraints(:ip => /192.168.\d+.\d+/) do
    resources: posts
end
```

If your subdomain is more complex than the above example then you can create your own class for it which is what this book walks you through doing.
