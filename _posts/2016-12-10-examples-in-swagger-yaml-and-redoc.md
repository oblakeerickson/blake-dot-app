---
layout: post
title:  "Including Examples in Swagger YAML and ReDoc"
date:   2016-12-10 01:00:00 -0600
---

I'm currently working on documenting the entire Discourse API into swagger yaml
files. Once I figured out the basic swagger rules to follow it has been pretty
smooth sailing.

One thing that has been missing though is including examples in the
documentation, but I figured that out this morning :)

Before I would do something like this:

```
...
properties:
  top_menu:
    description: pipe delimited
    type: string
...
```

which would generate output like this on the ReDoc page:

```
{
    "top_menu": "string"
}
```

But since we are passing in a pipe delimited string, I think it would be helpful
to include what that looks like. Apparently all you have to do is include an
`example` property on `top_menu` like:

```
...
properties:
  top_menu:
    description: pipe delimited
    example: latest|new|unread|top|categories|read
    type: string
...
```

which will look like this on the ReDoc page:

```
{
    "top_menu": "latest|new|unread|top|categories|read"
}
```

Including an example is much more helpful this just "string".
