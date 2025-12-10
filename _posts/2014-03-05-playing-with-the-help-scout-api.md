---
layout: post
title:  "Playing with the Help Scout API"
date:   2014-03-05 01:00:00 -0600
---

Help Scout offers a great service for teams to share a single inbox and they also provide an API if you need to further integrate with their service.

To get started all you need is an API Key which you can get after signing up from your profile page under the API Keys section.

Help Scout provides some API Wrappers in [PHP](https://github.com/helpscout/helpscout-api-php) and [Java](https://github.com/helpscout/helpscout-api-java), but there is also an unofficial API Wrapper in [Ruby](https://github.com/hramos/helpscout) that I've been using.

Currently I'm working (as in I just started 1 hour ago) on [a small little utility](https://github.com/oblakeerickson/helpscout-email-timer) that will track how long it takes for emails to get processed by Help Scout's email servers and show up inside of the app. There are of course lots of other things you can use the API for, such as metrics on what your response time is to emails.
