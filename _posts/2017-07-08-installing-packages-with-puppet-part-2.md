---
layout: post
title: "Installing Packages with Puppet Part 2"
date: 2017-07-08 06:00:00
---

In my [previous post][] we installed a single package, but if you are installing
lots of packages that don't need any customization it would probably be better
to wrap them all in a single module.  This post will show you how to do just
that.

There are several ubuntu packages that we would like installed as part of our
base system and none of them really need any special configuration once they are
installed so let's group them all into one module.

Inside of your modules folder create a folder called `base-apps` and create
a file called init.pp:

```
mkdir -p modules/base-apps/manifests
touch modules/base-apps/manifests/init.pp
```

Now edit `init.pp` with the following code. First we are going to create a class
and call it `base-apps`. Then we are going to create a single array containing
all the packages we would like to install. Then we can reference the entire
array and ensure all those packages are installed.

```ruby
class base-apps {

  $base_apps = [
    'silversearcher-ag',
    'curl',
    'expect',
    'python-software-properties',
    'debconf-utils',
    'git-core',
    'build-essential',
  ]

  package { $base_apps:
    ensure => installed,
  }

}
```

Now open up your `manifests/site.pp` file and add

```
include base-apps
```

to the default node.

Then save, commit, and push your changes. The next time the cron job runs on
your server it will pull down the changes and install all those packages.

[previous post]: {{ site.baseurl}}{% post_url 2017-05-20-installing-packages-with-masterless-puppet %}
