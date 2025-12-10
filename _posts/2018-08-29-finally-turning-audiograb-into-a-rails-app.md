---
layout: post
title: "Finally Turning AudioGrab Into a Rails App"
date: 2018-08-26 06:00:00
---

#### 6:45 PM

Okay today I'm finally going to make a Rails app for AudioGrab. I think creating
a cli app was a great first step, but having a rails app that I could have a
bookmarklet talk to is what I really want. The [original audiograb][orig] I made
back in 2013. My current [cli version][curr] I just opened sourced.

My goal for tonight is to make the most basic rails app and get it deployed to
production. All I want it to do is have an input box for the youtube url with a
submit button. It then will take that url and download the youtube video,
convert it to mp3, and then upload it to my overcast account.

This means that I won't have user accounts yet, but maybe I can just protect it
with basic auth or something.

#### 7:08 PM

Okay I just ran `rails new audio_grab_app` to generate my new app, ran `rails
server` to verify that it runs, and now I'm going to push it up to github.

Okay I created my public repo on github and added a license.

Then I ran `git remote add origin <repo-name>`. Followed by `git pull --rebase
origin master` to pull down my license. Then I [committed][commit1] and pushed my current
changes.

Okay now its dinner time.

#### 9:17 PM

Now that I'm back from dinner and playing bed wars with my 9 year old, let's see
if we can write some rails code.

`bin/rails generate controller Links create`

Oops I probably should create the new action for my form and make that the first
page you go to. Create will handle the form submission.

Okay I just created new.html.erb and changed the route in routes.rb to `get
'links/new'.

Now I need to make my form. I'm not going to persist anything to the database
yet for this because I don't want to remember any of these links. So I'm going
to create a new Link model, but not have it inherit from active record.

So my model class is called Link and I was also going to call my value I'm
storing called link as well, but I think that will get confusing so I'm going to
just call it url.

Okay my form is working and I'm able to submit it. Now I need to hook up all the
stuff in my command line app after the form is submitted, but first I'm going to
[commit][commit2] what I have so far.

#### 11:02 PM

Just got back from a walk. I think the first thing I need to do is be able to
load some secrets for overcast. For obvious reasons I don't want them to be
checked into source control, but I need my controller or rake task to be able to
read from them.

Ohh maybe I can use the new credentials feature:

https://medium.com/@wintermeyer/goodbye-secrets-welcome-credentials-f4709d9f4698

Maybe I should also watch (or listen) this YouTube video on the subject:

https://www.youtube.com/watch?v=fS92ZDfLhng

Okay, cool I got credentails working. What I want to happen is create a
background process to download and the YouTube video so that the web page
doesn't stay open forever if I had it do all the work in the controller. I don't
really want sidekiq right now, so I think I can just do this in a rake task or
something. Maybe I could use [Active Job][aj]?

Sweet I just created my active job called ProcessVideo and pretty much just
copied what I had in this [initial commit][ic] from audio_grab.

youtube-dl ran just fine and created a .mp3 file at the application root. I
wonder if I should store it in the `/tmp` directory? I then ran into an error I
think trying to load the file. Ohh I see what I did. The variable was still
called files instead of just file. I also just changed it to use the `/tmp`
directory instead. Let's see if it runs this time.

Wow it actually worked. My form returned right away while it processed the video
in the background and then uploaded it to overcast.

There are still some improvements like making sure I don't just grab the first
.mp3 file from the tmp directory but the actual video that was downloaded incase
I'm in the middle of processing multiple videos.

Also I still need to deploy it, but I'll have to do that another day. Here is my
[last commit][lc].

[orig]: https://github.com/oblakeerickson/audiograb
[curr]: https://github.com/oblakeerickson/audio_grab
[commit1]: https://github.com/oblakeerickson/audio_grab_app/commit/a2800d55de4a144266fa7ca98d00e547527bb9b0
[commit2]: https://github.com/oblakeerickson/audio_grab_app/commit/14b17f804f68732bd9544c358766508e8abf68e7
[aj]: https://edgeguides.rubyonrails.org/active_job_basics.html
[ic]: https://github.com/oblakeerickson/audio_grab/commit/cbf6f344ce606b73f2d2c615bc803382216b3110
[lc]: https://github.com/oblakeerickson/audio_grab_app/commit/06cfa9052277725a94614e4b2310e5fc0102380c
