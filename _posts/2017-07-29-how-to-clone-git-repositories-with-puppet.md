---
layout: post
title: "How to Clone Git Repositories with Puppet"
date: 2017-07-29 06:00:00
---

In this post we are going to learn how to clone git repos with puppet using the
vcsrepo module. Please refer to the [previous post][] about manually installing
puppet modules for more info on that subject.

I tend to make lots of git repos for lots of little code projects I work on,
but I'm not very good about keeping them in sync between two computers.
Sometimes I'm good about pushing them up to github, but usually they just live
on one computer and then they probably end up getting lost forever whenever I
re-install my OS or upgrade computers. One way I hope to remidy this problem is
to add all the repos I work on to puppet, that way puppet will pull down the
repo from github for me. I should probably work on some tool to notify me if
certain repos aren't on github yet.

### Installing the vcsrepo module

Because I have a masterless puppet setup I'm going to manually install this
module. Be sure to check the [metadata.json][] file to make sure the version
you are installing will work with your version of puppet and be sure to also
install any dependencies listed in that same file.  Because I'm still using
puppet 3.8 for my dev environment I need to install [vcsrepo version 1.5.0][].

To install it go to the [releases page][] and download the zip or tar.gz file
for the version that you need. Then extract it into your external modules
puppet folder. Be sure to rename the directory so that it is just 'vcsrepo' and
not the full 'puppetlabs-vcsrepo' name.

### Cloning a git repo

Okay, now that we have the vcsrepo module installed, lets use it. Here is an
example:

```ruby
class code {

  vcsrepo { '/home/blake/code/discourse_api': 
    ensure   => present,
    provider => git,
    source   => 'https://github.com/discourse/discourse_api.git',
    user     => 'blake',
  } 

} 
```

Now let's break it down a bit. The `provider` option lets vcsrepo know to use
git because it actually has support for other version control systems. The
`source` options is just the url for git repo. In another post I'll write up
how to clone a private git repo where you have to provide an ssh key. The
`user` option is so that puppet will clone this repo as the specified user
instead of as root.

Puppet will only to a git clone if this directory doesn't exist on my system.
This is nice just in case I have pending changes puppet won't overwrite them.
If you would like puppet to always to a git clone and overwrite any changes you
can use the `ensure   => latest,` option.

[previous post]: {{ site.baseurl}}{% post_url 2017-07-22-manually-installing-puppet-modules %}
[metadata.json]: https://github.com/puppetlabs/puppetlabs-vcsrepo/blob/master/metadata.json
[vcsrepo version 1.5.0]: https://github.com/puppetlabs/puppetlabs-vcsrepo/blob/cf089d78437279c6f24925a1c38d628910ef2d2c/metadata.json#L75
[releases page]: https://github.com/puppetlabs/puppetlabs-vcsrepo/releases

