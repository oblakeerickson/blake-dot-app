---
layout: post
title: "Weekly Journal #2 - Feel It Still"
date: 2017-10-29 06:00:00
---

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="7" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50.0% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAMUExURczMzPf399fX1+bm5mzY9AMAAADiSURBVDjLvZXbEsMgCES5/P8/t9FuRVCRmU73JWlzosgSIIZURCjo/ad+EQJJB4Hv8BFt+IDpQoCx1wjOSBFhh2XssxEIYn3ulI/6MNReE07UIWJEv8UEOWDS88LY97kqyTliJKKtuYBbruAyVh5wOHiXmpi5we58Ek028czwyuQdLKPG1Bkb4NnM+VeAnfHqn1k4+GPT6uGQcvu2h2OVuIf/gWUFyy8OWEpdyZSa3aVCqpVoVvzZZ2VTnn2wU8qzVjDDetO90GSy9mVLqtgYSy231MxrY6I2gGqjrTY0L8fxCxfCBbhWrsYYAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://www.instagram.com/p/Ba1diaTFoKf/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_blank">Just thought I’d share another Fall photo before all the leaves are gone! #yellow #sunset</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">A post shared by Blake Erickson (@oblakeerickson) on <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2017-10-29T14:30:21+00:00">Oct 29, 2017 at 7:30am PDT</time></p></div></blockquote>
<script async defer src="//platform.instagram.com/en_US/embeds.js"></script>

I can't believe that Halloween is almost here and all the leaves on the trees
are going to be gone. I went on a nice long walk yesterday with Hailey since the
weather was so nice, but I feel like that is going to be the last walk of the
year where we won't have to bundle up to go outside.

Dash also had his last soccer game this weekend. It has been a lot of fun
watching him progress this year. I still remember his first practice this season
when he was so confused trying to learn how to throw the ball in over his head.

### Work update

This week was another week filled with Elasticsearch. I worked on upgrading our
2.4 cluster to 5.6.3 and figuring out all the different aws settings that are
needed for the `elasticsearch.yml` file. I also created our own very basic
docker image, [elasticsearch-aws][1] for added in the discovery-ec2 plugin to the base elasticsearch
docker image. I also worked on some puppet changes and learned some more about
how Hiera works.

### SkillSift Update

This week I setup SSl for the main [SkillSift Website][2] which was suprisingly
easy. I also started working on setting up a Jekyll blog that will replace the
current home page which is just a single `index.html` file. I feel like every
successful product/bussiness needs a blog that updates regularly, so I figured I
should start now even though the app isn't anywhere close to being finished. I
also worked on the SkillSift app a bit and started working on the login/signup
functionality.


### Personal project updates

TinyTodo got some updates this week as well. I'm still not sure what my long
term plans are for TinyTodo, but I mostly have it as a playground to sharpen my
programming skills. Some of my updates from this week:

- Add links to the nav bar
- Allow only one user to signup (It's a single user application)
- be able to edit list titles

This week While running at the gym I would watch/listen to the aws
[acloud.guru][10] course. I still haven't fully committed to getting my aws cert
yet, but the things that I'm learning have been very helpful.

### Podcasts

I usually end up listening to quite a few podcasts every week either while I
workout or while I do chores around the house, so I thought it would be a good
idea to share some of the ones I've listened to and one link or highlight from
it.

#### [The Art of Product - 21: Launching Refactoring Rails][4]

It's always nice to hear Ben's updates about his [Refactoring Rails][5] course
and how well it is doing, but I think it is important for us to notice that he
has been working on his peronal brand for some time before this course even came
out. He has had a public influence on the ruby community working at thoughtbot,
has spoken at many conferences, has had a podcast for a couple of years now, and
an email list with hundreds of subscribers. It is just someting more for me to
remember as I'm trying to launch my own app and I haven't done any of those
things.

Derrick finally announced the project he will be using Elm for. I'm also pretty
curious about using Elm, but I'm still very interested in Ember and still want
to keep learning that before I learn yet another js tool.

#### [ember weekend - 118: Progress Report][6]

Speeking of ember, I just discovered this podcast this week! A quick podcast
that will help keep you updated with the lastest ember news.

#### [JSJ 284: Helping Developers Build Healthy Bodies][7]

I haven't listend to this podcast for a while, but I am very interested in
trying to stay healthy so that I can be a more productive programmer. One of my
take aways from this episode is to drink more water and so I'm going to try and
drink 1 gallon every day. How much water should we be drinking every day any
ways?

### Discourse Forums

Every now and then I find Discourse forums out in the wild that I didn't know
existed. Here are two that I found this week:

- [Ubuntu Community][8]: The meeting point for the Ubuntu community.
- [Balsamiq Community Discussion][9]: User Forums for Balsamiq Products.

[1]: https://hub.docker.com/r/discourse/elasticsearch-aws/
[2]: https://www.skillsift.com
[4]: http://artofproductpodcast.com/episode-21
[5]: https://www.refactoringrails.io/buy
[6]: https://emberweekend.com/episodes/progress-report
[7]: https://devchat.tv/js-jabber/jsj-284-helping-developers-build-healthy-bodies
[8]: https://community.ubuntu.com/
[9]: https://forums.balsamiq.com/
[10]: https://acloud.guru/
