---
layout: post
title:  "Modify etc/hosts file with node.js"
date:   2016-10-16 01:00:00 -0600
---

I've been manually updating my etc/hosts to add subdomains for an app that I'm
working on, but now I'm on a new computer and I needed to re-setup my etc/hosts
file so I figured I should create a bin/setup.js file to automate the process
and ensure that I don't have to manually configure anything to get my tests to
pass.

To edit my hosts file with node I decided to try and use
[hostile](https://github.com/feross/hostile).

It was pretty easy to use:

```
npm install hostile --save

```

Then in your js file:

```
var hostile = require('hostile');

var subdomains = ['one', 'two', 'three'];

subdomains.forEach(function (sd) {
  hostile.set('127.0.0.1', sd + '.myapp.local', function (err) {
    if (err) {
      console.log(err);
    } else {
      console.log('added: ' + sd);
    }
  });
});

```

So far the only downside to using node for this is that it requires root access
and I don't want to give node root access. I'm sure this is pretty bad too (but
way less worse) I just gave my user permission to edit the /etc/hosts file:

```
sudo chown blake /etc/hosts
```

Since my app is also going to need to setup up subdomains dynamically  as users sign up it
might be better to use something like
[dnsmasq](http://stackoverflow.com/a/20446931/588458) and just use a wildcard route to
map all subdomains to my route and not worry about adding individual entries to
the /etc/hosts file.
