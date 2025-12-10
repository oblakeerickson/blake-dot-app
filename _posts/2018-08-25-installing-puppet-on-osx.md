---
layout: post
title: "Installing Puppet on OS X"
date: 2018-08-25 06:00:00
---

My main computer right now is a Linux based desktop computer, but my laptop is a
13" MacBook Pro running the latest version of OS X. Because I use my desktop the
most I feel like whenever I do need to be portable and grab my laptop, it is
always out of sync with my desktop. Then rather than being productive and
getting done what I need to get done I spend my time configuring my laptop.

I've been trying to be really good with my current desktop and configure
everything via puppet, my goal is that I can also puppettize my OS X based
laptop, so I set out to do just that today. I didn't realize that full support
for Puppet and external modules really is only on Linux distros, but they do
have an official OS X installer, so this is looking promising.

To install Puppet on OS X visit the offical [Installing Puppet agent: MacOS][ip]
page. And on step #2 click the package link that takes you to [this
download][dl] page. Actully just visit this [/mac/puppet/10.13/x86_64][ftp] page
and download [puppet-agent-latest.dmg][dmg].

This will download the puppet agent installer. Click on it and follow the
install instructions. I'm actually running a masterless puppet install so I
don't actually need the puppet agent running. Once puppet is installing you can
then turn off the puppet agent with this command:

    sudo puppet resource service pxp-agent ensure=stopped enable=false

You can also verify that puppet is installed by running:

    puppet --version

Now you can browse to `/etc/puppetlabs` and edit your puppet config.

[ip]: https://puppet.com/docs/puppet/5.3/install_osx.html
[dl]: https://downloads.puppetlabs.com/mac/
[ftp]: https://downloads.puppetlabs.com/mac/puppet/10.13/x86_64/
[dmg]: https://downloads.puppetlabs.com/mac/puppet/10.13/x86_64/puppet-agent-latest.dmg
