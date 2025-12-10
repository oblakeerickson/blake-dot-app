---
layout: post
title:  "Update Column"
date:   2014-03-11 01:00:00 -0600
---

Tonight I worked on updating a single attribute for an existing User. While I think there is still probably room for some improvement, I do have the basic functionality down. There are several rails methods that you can use to update a User in your database, `update_attributes`, `update_attribute`, `update_column`, plus some others.

I ended up going with `update_column` because it doesn't talk to my Model and perform a validation. Right now this is the only way I could get it to work since I don't want it to update all the other User attributes.
