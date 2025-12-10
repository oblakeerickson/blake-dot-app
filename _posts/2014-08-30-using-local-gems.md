---
layout: post
title:  "Using Local Gems"
date:   2014-08-30 01:00:00 -0600
---

Today I started working on adding some features to the [discourse_api](), but I needed to work on the gem locally and rebuild it to test my changes. Using a gem locally took me a lot longer than I wanted to spend today, so I thought I'd write up how to do it.

First of all I would delete the gem that you might have installed from ruby gems already:

```
gem uninstall discourse_api
```

Then clone a copy of the gem

```
git clone https://github.com/discourse/discourse_api.git
```

Create a project folder for you new app

```
mkdir app
```

Inside of our `app` directory create a `Gemfile` with the contents:

```
source 'https://rubygems.org'
gem 'discourse_api', :path => '/full/path/to/discourse_api'
```

As you can see we specified a `:path` pointing to where the gem can be found locally. Now type:

```
bundle install
```

Once of the lines of output from the `bundle install` command will be:

```
Using discourse_api 0.2.1 from source at /vagrant/discourse_api
```

This way you can tell it grabbed a local version of them gem and not one from rubygems.org.

Now create a file called `app.rb` with the contents:

```
require "discourse_api"

client = DiscourseApi::Client.new("https://meta.discourse.org")
puts client.user('oblakeerickson')
```

Now to run it you need to type `bundle exec ruby app.rb` instead of just `ruby app.rb`:

```
bundle exec ruby app.rb
```

Hopefully remembering to specify a `:path` and to use `bundle exec` will make using a gem locally much easier for you.
