---
layout: post
title:  "Masterless Puppet on Ubuntu 16.04"
date:   2017-03-06 01:00:00 -0600
---

This tutorial is adapted from [this
article](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-masterless-puppet-environment-on-ubuntu-14-04)
where we will cover Installing a Masterless Puppet configuration on Ubuntu 16.04
using GitHub.

You can setup a fresh Ubuntu 16.04 box on
[DigitalOcean](https://m.do.co/c/6181643725e8) or you can setup
[VirtualBox](https://www.virtualbox.org/) and run a VM locally.

### Step 1: Installing Puppet and Git

On a fresh Ubuntu 16.04 box run [these
commands](https://docs.puppet.com/puppet/latest/puppet_collections.html#apt-based-systems)
as root so that we can install puppet:

```
wget https://apt.puppetlabs.com/puppetlabs-release-pc1-xenial.deb
dpkg -i puppetlabs-release-pc1-xenial.deb
apt update
```

Then install puppet and git with this command:

```
apt install puppet git-core
```

### Step 2: Setting up the git repo

We are going to add a deploy key to a new GitHub repository that we will create
in just a bit but first we need to create a ssh key on our new Ubuntu box.

Run this command and press 'enter' several times to accept all the defaults:

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Once your key has been created let's copy it so that we can add it to GitHub:

```
cat ~/.ssh/id_rsa.pub
```

with your mouse copy the output to your clipboard.

Go to github.com and create a repository. Then go into the settings for that
repo and add a deploy key. Give it a title, paste in the public key, check the
"Allow write access" for now, and finally press "Add key".

Finish setting up git with these commands

```
git config --global user.email "you@example.com"
git config --global user.name "Your name"
git config --global core.editor "vim"

```

### Step 3: Pushing the Initial Puppet Configuration

```
cd /etc/puppet
git init
git add .
git commit -m "initial commit"
git remote add origin git@github.com:<username>/<repo>.git
git push origin master
```

### Step 4: Edit puppet config

Change `/etc/puppet/puppet.conf` to:

```
[main]
logdir=/var/log/puppet
vardir=/var/lib/puppet
ssldir=/var/lib/puppet/ssl
rundir=/run/puppet
factpath=$confdir/facter

```

Notice that we changed `$vardir` to
[`$confdir`](https://docs.puppet.com/puppet/4.9/dirs_confdir.html).

```
cd modules
mkdir -p cron-puppet/manifests cron-puppet/files
vim cron-puppet/manifests/init.pp
```

Add this to the `init.pp` file:

```
class cron-puppet {
  file { 'post-hook':
    ensure => file,
    path   => '/etc/puppet/.git/hooks/post-merge',
    source => 'puppet:///modules/cron-puppet/post-merge',
    mode   => 0755,
    owner  => root,
    group  => root,
  }
  cron { 'puppet-apply':
    ensure  => present,
    command => "cd /etc/puppet; /usr/bin/git pull origin master",
    user    => root,
    minute  => '*/1',
    require => File['post-hook'],
  }
}

```

Now edit `cron-puppet/files/post-merge`:


```
#!/bin/bash -e
## Run Puppet locally using puppet apply
/usr/bin/puppet apply /etc/puppet/manifests/site.pp

## Log status of the Puppet run
if [ $? -eq 0 ]
then
  /usr/bin/logger -i "Puppet has run successfully" -t "puppet-run"
  exit 0
else
  /usr/bin/logger -i "Puppet has ran into an error, please run Puppet manually" -t "puppet-run"
  exit 1
fi

```

Finally, we have to tell Puppet to run this module by creating a global
manifest, which is canonically found at /etc/puppet/manifests/site.pp.

```
node default {
  include cron-puppet
}
```

Now run:

```
puppet apply /etc/puppet/manifests/site.pp
```

and hopefully you don't see any errors.

Now commit you changes and push them up to GitHub. Now you can pull this repo
down to your local computer, make changes, push them back up to GitHub, and
they will automatically be applied to your server.

