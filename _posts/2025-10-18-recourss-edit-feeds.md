---
layout: post
title: "Recourss Edit Feeds"
date: 2025-10-18 01:00:00 -0600
---

Today I worked on the edit feed feature in [Recourss][1]. This will allow you to rename a feed, fix the feed url, and also see when it was last fetched.

![recourss-edit-feed](/assets/images/edit-feed.png)

This will allow you to easily see which feeds are stale. I should probably add some sort of sort feature next. You can also see if a feed has never been fetched which means the url is probably bad.

The last change I made was I removed the link from the feed url so that it is just rendered as text. Clicking on the rss feed url isn't usually very friendly as your browser will either open up the giant xml file, download it, or complain. I then added a url though to the feed name that takes you to all the posts for the specific feed.

It's nice to keep polishing an app I'm working on and currently using. Hopefully I can keep making it a little bit each day.

[1]: https://app.recourss.com
