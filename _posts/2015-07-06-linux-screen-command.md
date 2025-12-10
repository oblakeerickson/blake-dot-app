---
layout: post
title:  "Using the Linux Screen Command"
date:   2015-07-06 01:00:00 -0600
---

I use [Digital Ocean][1] for hosting many different Linux servers that I have:
[longeststreak.net][2], [this website][3], a private [Discourse][4] forum, a
private [minecraft][5] server, and one I use for programming (the one I'm using right
now to write this post). The point I'm getting at is that I end up SSH'ing into
these boxes a lot and one tool that I use every time is the `screen` command.

Screen allows you to connect back to the exact same terminal you were on in case
your connection got lost while writing in vim. Another example is so that you
can start a process like minecraft and not have to use the `&` symbol for it to
run in the background.  

Screen also allows you to create windows so that if you need another shell on
the same box you don't have to ssh in again.

Here are the screen commands that I use most often:

- `screen` - starts a new screen session
- `ctrl-a d` - detaches from screen
- `screen -ls` - shows a list of screen sessions
- `screen -D` - detach an active screen (necessary if you connection is lost and
  you are SSH'ing back into the box)
- `screen -r` - re-attach to screen session
- `ctrl-a c` - create a new screen window
- `ctrl-a n` - switch between screen windows

The point of this post is not to give an exaustive tutorial on `screen`, but to
make you aware that it exists and give you a few commands to help you get
started. If you aren't using `screen` yet I hope you can start.

[1]: https://www.digitalocean.com/?refcode=6181643725e8
[2]: http://longeststreak.net/
[3]: http://blaketv.com
[4]: http://www.discourse.org/
[5]: https://minecraft.net/ 
