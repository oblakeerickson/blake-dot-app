---
layout: post
title: "Weekly Journal #6 - Community"
date: 2017-11-26 06:00:00
---

This past week was Thanksgiving and I got to make the turkey again this year. I
don't cook all that often but even though it is a lot of work I do enjoy being
in charge of the turkey. It was also nice to have some friends and family over
since we were hosting. Also one of the best parts of Thanksgiving is all the
pie. My favorite pie this year was the coconut cream pie my mom made.

### Work update

This was a short week for me work wise since I took Thursday and Friday off, but
I felt like it was a pretty good week. I was most excited by the fact that I got
my Grafana graphs working in my aws dev environment so that I could see the
performance of my test Discourse forum and really start tuning it and see how
much traffic it can handle.

### SkillSift Update

For [SkillSift][4] I was able to create a separate view for the job listings for
public users and admin users. The admin side will be for creating, deleting, and
editing job listings and the public view will be the main job board page that
will be styled nicely. I still haven't figure out if I want all the routes that
require a login to be behind a `/admin` route. One reason I don't like this
logic is that I plan to have some users that will be conducting interviews but
they might not be admins so it seems weird that they will be accessing pages
that are nested behind the `/admin` routes.

One of my goals for SkillSift is much more than just the SaaS app, but to build
a community around hiring. I really am not sure why, but for some reason I just
love processes and how companies work. One of my favorite tv shows is The
Profit, probably because I enjoy seeing how the companies improve after Marcus
Lemonis adds processes to the businesses he invests in. I think that one way
businesses can improve and be successful is through improving their hiring
process.

### Personal projects Update

I was not able to make progress on TinyTodo, but I have been using it here and
there to keep track of things. One problem I would like to solve is that I keep
having to re-log in every day because my session cookie or something is
expiring.

I would really like to get my aws certification and even my azure certification,
so this week I would like to actually start working torward my aws cert. Even if
it is just a little bit, I think it would be really good for me to make prgress
on.

### Podcasts

A couple of podcast episodes that I would like to highlight are:

- [Giant Robots: Product and Vision (Chris Savage & Brendan Schwartz)][1]
- [Eat Sleep Code: Finding Your Developer Community][2]

### Discourse Forums

I have a very hard time reading through email lists, so one of the new Discousre
sites I'm excited about is actually a mirror of an email list:

- [Ruby Talk Mailing List Mirror][3]

I also really like that Discourse can continue to support the Ruby community
even if it is just a little way like this.

[1]: http://giantrobots.fm/254
[2]: https://overcast.fm/+E3lWUQX_M
[3]: https://ruby-talk.trydiscourse.com/
[4]: https://skillsift.com
