---
layout: post
title: "Installing Packages with Masterless Puppet"
date: 2017-05-20 06:00:00
---


My first post on [Masterless
Puppet]({{ site.baseurl }}{% post_url 2017-03-06-masterless-puppet-on-ubuntu-16-04 %})
walked us through setting up puppet in a masterless setup, but we didn't
actually use it to install any software package or files to configure our
server, which is the whole point of puppet, so let's do that now.

For this example we are going to install a very handy apt package called
'silversearcher-ag' which is just a faster replacement for ack and most likely
is not installed by default.

**(1)** Create a new folder inside of modules and call it `ag`. Create another
folder inside of `ag` called `manifests`. This should look very similar to the
previous `cron-puppet` folder we already created.

{% highlight bash %}
mkdir -p modules/ag/manifests
{% endhighlight %}

**(2)** Inside of the `modules/ag/manifests` folder create a file called
`init.pp` with the following contents

{% highlight ruby %}
class ag {
  package { 'silversearcher-ag':
    ensure => installed,
  }
}
{% endhighlight %}

**(3)** Now we need to tell puppet that we would like this module to be ran
when the `puppet apply` command is ran. Open up the existing
`manifests/site.pp` file and add our new module to it:


{% highlight ruby %}
node default {
  include cron-puppet
  include ag
}
{% endhighlight %}


**(4)** Now we can commit our changes and push them do our git repo. Once the
cron job runs again on our server it will pull down these changes and puppet
will apply them. Once that is done you should now have access to the `ag`
command on the server!

So I don't think we are going to want to create a new module for every single
package we are going to install, so we probably will want to pick a more
generic name than 'ag' so that we can install multiple packages with one
manifest file.

I think one of the next projects I want to work on is configuring my dev
environment with puppet. I currently have a desktop and a laptop and I would
like to be able to keep them in sync so that whenever I want to get work done
on my laptop I can actually get work done and not have to configure it so that
it is setup just like my desktop.

