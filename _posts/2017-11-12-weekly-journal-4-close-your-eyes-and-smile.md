---
layout: post
title: "Weekly Journal #4 - Close Your Eyes and Smile"
date: 2017-11-12 06:00:00
---

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50.0% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://www.instagram.com/p/BbU5qPnFGkb/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_blank">Lunch time with Dashio pistachio!</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">A post shared by Blake Erickson (@oblakeerickson) on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2017-11-10T19:32:32+00:00">Nov 10, 2017 at 11:32am PST</time></p></div></blockquote> <script async defer src="//platform.instagram.com/en_US/embeds.js"></script>

So far my new big rocks schedule has been working out really well, but like
always there are still some improvements I can make. I want to get better at
having some longer periods of focus time and be better about avoiding
distractions. This week I was able to make it to the gym regularly and still
feel productive at work and get 8+ hours in every day which is not always easy
when you are juggling in kid schedules. I do appreciate every day though that I
get to eat lunch with Dash and walk him to school. Next year when he is is 1st
grade all day I'm sure I will look back on these days and miss them.

### Work update

This week I got to learn and dig into grafana for the first time. I've only ever
looked at a couple of grafana dashboards before but never had to set one up. So
this week I worked on automating the setup of grafana dashboards and datasources
via puppet so that whenever we spin up a new datacenter or workspace grafana is
already setup and ready to go without any manual setup. Grafana has a nice rest
API that made this pretty easy to import saved json files.

Oh also this week our new [team page][6] live! It's crazy to think that in
Febuary of this year I was employee #11 and now we have 20 employees.

### SkillSift Update

This week I finished up the signup and login functionality. Which means I can
actually start working on some actual features for the app. My goal right now is
to finish up a very minimal feature set so that I can just say that I have
finally shipped. Then I can just keep iterating from there. As an example I
might only allow one user to login to administer their job board and review
applicants. I also worked some more on merging the current homepage into Jekyll,
but still have quite a bit of css and html to wrangle.

### Personal projects Update

I was able to fix a big bug with TinyTodo in production that was preventing me from using it
on multiple devices (well that's what I thought the issue was anyways). After I
finally had time to looks at the rails logs I came across this error:

> HTTP Origin header didn't match request.base_url

Turns out that enabling SSL in nginx was causing this error, but for some reason
my original browser that I have been using for development and even accessing
the production app wasn't throwing this error so it took me awhile to realize it
was happening.

[The solution][1] is to update your nginx config and make sure you are forwarding the correct
headers:

```
upstream myapp {
  server              unix:///path/to/puma.sock;
}
...
location / {
  proxy_pass        http://myapp;
  proxy_set_header  Host $host;
  proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header  X-Forwarded-Proto $scheme;
  proxy_set_header  X-Forwarded-Ssl on; # Optional
  proxy_set_header  X-Forwarded-Port $server_port;
  proxy_set_header  X-Forwarded-Host $host;
}

```

Another project that I'm working on is seeing if I can get Discourse to run on a
Raspberry Pi 3.  This weekend I was able to install Raspbian on a micro sd card
I swipe from my go pro and was able to get it to boot just fine. I can already
tell it is way faster than my Raspberry Pi 2. I was also able to get docker
running, but that's all the progress I was able to make, well besides building
an initial case for it out of Lego. Next on my list is to keep working on my
Dockerfile and get Ruby installed inside of Docker.

### Podcasts

Here are a couple of podcast episodes that I was able to listen to this week:

- [Complete Developer Podcast: Antipatterns In Distributed Teams][2]
- [Ruby Rogues 335: Collaborative and Effective Work Environment with David Richards][3]

### Discourse Forums

Every week I like to feature a Discourse forum. One of the forums that I'm
becoming a bit more active on is [Discuss Bootstrapped.fm][4]. It has a very
helpful community and many great topics for those wishing to bootstrap a side
project or startup.

This tweet that [Discourse][5] received this week was pretty cool!

<blockquote class="twitter-tweet" data-cards="hidden" data-lang="en"><p lang="en" dir="ltr">We&#39;re thankful to the <a href="https://twitter.com/discourse?ref_src=twsrc%5Etfw">@discourse</a> team for building a fantastic platform for quality discussions, which don&#39;t interrupt and don&#39;t suck time. Discourse is honestly better than Slack, Email lists, or traditional forums. Kudos!<a href="https://t.co/G9oobSjMnl">https://t.co/G9oobSjMnl</a> <a href="https://t.co/g35xNLeZLP">pic.twitter.com/g35xNLeZLP</a></p>&mdash; Dgraph Labs (@dgraphlabs) <a href="https://twitter.com/dgraphlabs/status/928820976254459904?ref_src=twsrc%5Etfw">November 10, 2017</a></blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

[1]: https://github.com/rails/rails/issues/22965#issuecomment-172929004
[2]: http://completedeveloperpodcast.com/episode-116/
[3]: https://devchat.tv/ruby-rogues/rr-335-collaborative-effective-work-environment-david-richards
[4]: http://discuss.bootstrapped.fm/
[5]: https://twitter.com/discourse
[6]: https://www.discourse.org/team
