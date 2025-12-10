---
layout: post
title: "Bug Crushing Adventure"
date: 2018-10-31 01:00:00 -0600
---

At [Discourse][discourse] we have a new "game" that we play where we have a running bug
crushing topic on our internal team Discourse site that is always assigned to
someone. If this topic is assigned to you then you need to look through the
application logs of all the sites that we host to find a bug and then fix it.
Once the bug is fixed, post a reply to the topic with the details and then
assign the topic to a new person. So far it has been working great and it has
given me, a developer who is often busy working on infrastructure related ops
work, an opportunity to commit more code changes to the core Discourse app. Also
this helps spread the bug fixing responsibility across many more team members so
it doesn't just end up being a couple people fixing all the bugs.

Yesterday was my turn. I actually found a bug that I noticed was
happening on a couple of sites. I then spent a large chunk of my day trying to
fix it and replicate it locally. The initial hard part was getting the plugin
installed locally with the right environment variables. Once I was able to debug
the code locally something just didn't add up. LIke this literally could not be
happening. After much frustration and even pairing with my awesome coworker we
figured out that this bug was actually [fixed 27 days ago][fixed]. So we then
checked the deploy history for those sites and sure enough those sites just
hadn't been deployed since then and didn't have the fix.

I guess the lesson to learn here is to check git blame to see the last time a
file I'm working on was last modified. Maybe I'll look into something like
[vim-fugitive][fugitive] so that it is easier for me to see the git blame
history without leaving my trusty editor.

The good thing about all of this is that I actually learned quite a bit about
the code base by "investing" all of this time trying to fix that bug.

Luckily I was able to find another bug (which I originally was going to talk
more about in this post) that was showing up in the logs and
[crush it][crushed].

[discourse]: https://discourse.org
[fixed]: https://github.com/discourse/discourse-backup-uploads-to-s3/commit/652267988416f2d922c595cab50a2b9823bacf51
[fugitive]: https://github.com/tpope/vim-fugitive
[crushed]: https://github.com/discourse/discourse/commit/589e3fcaa0c8fed0f6de6e61912c8cc577975ee0

