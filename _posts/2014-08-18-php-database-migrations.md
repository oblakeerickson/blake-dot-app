---
layout: post
title:  "PHP Database Migrations"
date:   2014-08-18 01:00:00 -0600
---

# PHP Database Migrations

In the legacy codebase that I'm working with we currently are using a very simple and very manual method of performing database migrations. Basically we are just keeping a timestamped file with the sql code that needs to be performed. This by the way is much better than not having anything.

Anyways we are at the point where we need something a lot better and rather than rolling my own database migration tool I thought I would see what else was out there. Looks like [Phinx](http://phinx.org/) will do exactly what I'm looking for and the great thing is that it isn't tied to any specific framework.

I've only browsed some of the docs and glanced at some of the code, but hopefully I'll get a chance to use it soon and hopefully integrate it into our legacy application.
