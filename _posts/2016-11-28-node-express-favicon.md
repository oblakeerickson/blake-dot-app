---
layout: post
title:  "Add a favicon to an express application "
date:   2016-11-28 01:00:00 -0600
---

I've been working on an express app with a GET route that accepts an id as a
parameter:


```
app.get('/:id', function(req, res) {
  //
});
```

The problem I ran into that took me awhile to figure out was that chrome was
hitting that route to try and load the `favicon.ico` file. So basically my app was
making one request to that route and chrome was making another request to that
same route, but was throwing an error because `favicon.ico` isn't a valid `id` in
my app.

To have express return a favicon.ico file I installed
[serve-favicon](https://github.com/expressjs/serve-favicon).

Your app should look something like this:

```
var express = require('express');
var path = require('path');
var favicon = require('serve-favicon');
var app = express();
app.use(express.static('public'));
app.use(favicon(path.join(__dirname, '..', 'public', 'favicon.ico')));


app.get('/:id', function(req, res) {
  //
});

app.listen(3000);
```

Then place your `favicon.ico` file inside of your `/public` directory.
