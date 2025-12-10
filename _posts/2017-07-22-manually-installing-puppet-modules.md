---
layout: post
title: "Manually Installing Puppet Modules"
date: 2017-07-22 06:00:00
---

If you are using a masterless puppet setup this post will walk you through how
to manually install puppet modules that you can then reference in your own
puppet modules. Using someone elses puppet modules can save you a lot of time
and can keep your own modules clean and simple.

Inside of my puppet git repo I have a folder called 'modules' for all of the
modules that I have written, but I don't want to clutter up that folder with
external modules, so I created a folder called 'external-modules'.

One external puppet module that is handy is the [stdlib module][].

Before we install it we need to make sure the version is compatible with our
puppet version and check to see if there are any dependencies. You can see this
info inside of the version 4.17.1 [metadata.json][] file

```
"requirements": [
    {
      "name": "puppet",
      "version_requirement": ">= 4.7.0 < 6.0.0"
    }
  ],
```

As you can see from the empty array this module doesn't have any dependencies:

```
"dependencies": [

  ]
```

Because I'm using puppet version 3.8 still, I'm actually going to install
version 4.17.0 which you can find on the [releases][] page.

To install the module follow these step:

```
cd ~/puppet-repo/external-modules
wget https://github.com/puppetlabs/puppetlabs-stdlib/archive/4.17.0.tar.gz
tar zxvf 4.17.0.tar.gz
mv puppetlabs-stdlib-4.17.0 stdlib
```

Notice that I renamed the module to just 'stdlib' and not 'puppetlabs-stdlib`.

Now we need to add our 'external-modules' directory to our 'puppet.conf' file,
by appending this line to that file:

```
basemodulepath=$confdir/external-modules:$confdir/modules
```

Now that our external module is installed we can simply use it inside of one of
our own moodules:

```
mkdir -p modules/my-test/{files,manifests}
touch modules/my-test/manifests/init.pp
```

Now edit 'init.pp' to look like:

```
class my-test {

  file { '/home/blake/test.txt':
    ensure => present,
  }

  file_line { 'test_line':
    path => '/home/blake/test.txt',
    line => 'hello blake',
  }

}

```

The `file_line` type is part of the stdlib module. Be sure to add the 'my-test'
module to your site.pp file:

```
include my-test
```

Now when you apply the manifest on your puppetized server the stdlib module will
be installed and the 'hello blake' line should be added to the 'test.txt' file.

[stdlib module]: https://github.com/puppetlabs/puppetlabs-stdlib
[metadata.json]: https://github.com/puppetlabs/puppetlabs-stdlib/blob/master/metadata.json
[releases]: https://github.com/puppetlabs/puppetlabs-stdlib/releases

