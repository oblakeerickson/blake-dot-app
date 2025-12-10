---
layout: post
title:  "Rake Tasks and Helper Methods"
date:   2014-01-24 01:00:00 -0600
---

UPDATE**: I made a big mistake in this post, read why [here](https://blog.blakeerickson.com/lib-directory).

As I mentioned [two weeks ago](https://blog.blakeerickson.com/its-okay-to-start-over) I started to rewrite my [longest streak app](https://github.com/oblakeerickson/longest_streak) so that it could be a Rails app and not just a command line ruby application. I'm not really rewriting it per say, more just putting my existing ruby code into the rails structure. Yesterday I worked on setting up my models. I have two right now, a user model and a contributions model. And this morning I worked on setting up a rake task for connecting to the GitHub API and getting user data. I was able to get my Rake Task to talk to my User model and to also talk to two helper methods that I created.

One of my Helpers is used for setting up my connection to GitHub called *connection_helper.rb*:

```
module ConnectionHelper
  class Connection
    .
    .
    .
  end
end
```
And to access it inside of my Rake task I simply call it like this:

```
connection = ConnectionHelper::Connection.new
```

### Problems with threads

In my original command line project I was using threads when I collect user data, but It appears I can't use threads inside of a Rake Task so I'm going to have to figure out another way because I'm pretty sure if I ever want my tasks to complete in a reasonable amount of time I'm going to have to use threading.
