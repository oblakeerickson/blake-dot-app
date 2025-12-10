---
layout: post
title:  "lib Directory"
date:   2014-01-25 01:00:00 -0600
---

[Yesterday](https://blog.blakeerickson.com/rake-tasks-and-helper-methods) I wrote about creating my rake task for the longest streak app, but I made a big mistake in putting the class files that will be fetching all the user and contribution info from GitHub from github into the *helpers* directory.

Esspecially since these files don't contain methods that the models or the controller will be accessing I decided to move them into the *lib* directory. I think another common place to put files like this would be inside of the *models* directory, but since these methods, as far as I know, won't be used in the web portion of this project helping to serve data to web pages so I think they belong in the *lib* directory. Hopefully I'm correct in this, and if I'm not please let me know!

### Including the *lib* directory

Now that I moved my files into the *lib* directory I need to be able to access them from inside of my rake task. To do this you need to inlclude the *lib* directory into Rails Load path which you can do by adding the line `config.autoload_paths += %W(#{config.root}/lib)` inside of *config/application.rb*:

```
.
.
.
  module LongestStreak1
    class Application < Rails::Application
      .
      .
      .
      config.autoload_paths += %W(#{config.root}/lib)
    end
  end
```

Here is a link to my [commit](https://github.com/oblakeerickson/longest_streak/commit/d4e762443a1a96ee804ee28cc4247065f6377172) on GitHub addressing this issue.
