---
layout: post
title: "Weekly Journal #7 - Construction"
date: 2017-12-03 06:00:00
---

I feel like it's been a crazy last few weeks, probably mostly because we hired
some contractors to finish the nightmare we started by trying to remodel our
bathroom. They've been working on it almost everyday for the past couple of
weeks, but they will finally be done this week! I'm just ready to not have
people in my house and to not have to go to Lowes anymore. I am so glad that we
ended up hiring someone though, because trying to do that ourselves was a good
lesson in learning that we should not be doing construction work.

### Work update

I was finally able to find a headless browser that I could use for load testing.
I went with [Puppeteer][4] which is maintained by the GoogleChrome team. One of
the bigger issues that I had to overcome this week was finding a good way to
handle errors with the test and Chrome leaving behind browsers instances and
using app all the memory and crashing my load testing boxes. My solution was to
configure ruby, which does a system call out to node, to just kill the processes
after 30 seconds if it still hasn't completed.

### SkillSift Update

Most of my work for SkillSift this week was done on Tuesday night while my
daughter was at Gymnastics practice for 1 hour and I was able to bring my laptop,
put headphones on and just focus. The main task I was able to complete was add
an application at the bottom of a job listing that you can apply to. Now its
starting to feel more like a real app since admins can create job listings and
anonymous users can see the job listings and apply for them.

### Personal projects Update

I didn't spend any time studying for my AWS exam like I wanted to. Yes I was
busy with lots of things, but the truth is I just didn't make time for it. Just
as a small example, I did watch several Ruby Conference videos that just came
out this week, but I didn't need to to watch those right now, I could have spent
some of that time watching a short aws video or something.

For my personal projects this week I dust off one of my older projects that I've
been meening to publish, AudioGrab. It downloads youtube videos (like conference
talks) and converts them to mp3, and then upload them to my podcast player
(Overcast), so that I can listem to them just like a podcast.

### Podcasts

This week a great podcast that I listened to was [The Art of Product episode 25:
Chaos, and Growing an Engineering Team][2].

Here are a couple quotes from the episode:

> I'm so glad to see you using Discourse and not setting up a Slack channel for
> this. - Derrick

> I'm not going to contribute to the Slack noise. - Ben

> Discourse is such a good piece of software. - Ben

Another good podcast episode to listen to is the [Complete Developer Podcast
119: Console Apps][3]. I personally just really love console applications and I
think they are a great place to start when experimenting with a new application
idea.

### Discourse Forums

The Discourse forum that I would like to highlight this week is the [code quality
challege][1]. Right now it is a free course that is using Discourse to engage
users to talk about each of the code quality challenges.

[1]: https://www.codequalitychallenge.com/
[2]: http://artofproductpodcast.com/episode-25
[3]: http://completedeveloperpodcast.com/episode-119/
[4]: https://github.com/GoogleChrome/puppeteer
