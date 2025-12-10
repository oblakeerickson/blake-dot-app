---
layout: post
title: "Omarchy for macOS?"
date: 2025-09-27 01:00:00 -0600
---

There has been a lot of chatter about [Omarchy][0] and how amazing it is. I'm sure it is great, but I currently have a brand new 16" M4 MacBook Pro that I love and every time I've purchased a non-Apple laptop I always regret it for various reasons. Usually it ends up being the trackpad, fan noise, battery life, or some audio issue with crappy speakers or terrible mic.

I'm not against trying Omarchy on some other spare computer I have, but for now I'm sticking with my trusty MacBook Pro for my main computer.

I've been pretty lazy lately with my dev setup and I have not been using vim, a fancy terminal, or any window manager. While things were working fine with my current setup I was definitely starting to feel the pain of managing windows when I had 5 different Cursor windows open, many different browsers open, and many different terminals. Basically it was super difficult to find the specific application window and using "Mission Control" was very messy. I even shared my screen once on a work call to demo something and my coworkers got to see a glimpse of the craziness of my work environment. I wasn't really embarrassed by it, but it made me realized how chaotic my single mac workspace was getting.

I've been looking to improve my computer setup without feeling like I have to ditch my mac and switch to Omarchy even though it is the cool thing at the moment.

So how can you achieve the Omarchy like experience on macOS? I'm getting pretty far using only these 4 apps:

- [Aerospace][3] (a tiling window manager)
- [Ghostty][4] (a better terminal)
- [tmux][5] (a terminal multiplexer)
- [Neovim][6] (a terminal based editor)

Actually the only thing not included in Omarchy is just Aerospace, everything else like Ghostty, tmux, and nvim are included in Omarchy. Omarchy uses Hyprland for a window manager which is Linux only.

### [Aerospace][3]

The first thing to setup is Aerospace a tiling window manager for macOS. This is the first thing that I've changed with my workflow and its been great. The learning curve for some basic commands has been minimal and I've able to keep all my windows organized and easily switch between them using a couple of key strokes which has been way faster and easier than using Mission Control and trying to find a specific application window.

### [Ghostty][4]

I've been using iTerm2 for years now, but I did switch to Ghostty. That really hasn't been a huge transition either and its been working great. The remaining two items tmux and nvim have quite the learning curve and I still have some setting up to do to get fully moved over to both.

### [tmux][5]

While Ghostty has been easy to switch to, what hasn't been super easy is using tmux inside of Ghostty. Mostly I just open a ton of terminal tabs inside of a single terminal window which I have been basically been doing inside of tmux, but it has also been nice to do some split panes which I want to get in the habit of doing more of. My leader key is also still the default `ctrl+b` which isn't the easiest to always use so I might switch it to something like `capslock`. A couple of things you will need to configure for tmux is the ability to copy text out of the pane, scroll with the mouse, and also adjust the history-limit so that you can easily scroll through debug output like when using `bin/rails s`.

### [Neovim][6]

Neovim has also been difficult to get fully up and running in so I'm still using Cursor at the moment for my development work. I initially did install the [LazyVim distribution][1] but found it to be way too much, so now I'm currently rocking a very vanilla Neovim setup with the [lazy.vim][2] plugin manager. I really hate that they are basically called the same thing, very confusing. I've used vim a lot in the past and was very used to my previous setup and plugin manager so switching to Neovim has actually been quite difficult as it seems way more complex than whatever I was doing previously with a single `.vimrc` file.

I also use homebrew as the macOS package manager, but I've always been using that so that wasn't really anything to transition to.

And that's my current developer setup on macOS. I'm sure I'll keep expanding it to include more [keyboard-everything options][7], but for now I've been pretty happy with my setup and sticking with my trusty MacBook.

#### UPDATE 2025-09-29

I just discovered this great post about [dhh bashing on programmers who use Windows][8] back in 2008. So not much has really changed. Just a different flavor of OS to hate on.

I absolutely love this quote in response which sums up exactly my original intent of this blog post:

> **Don’t waste time arguing about the character select screen.** Results speak loudest. Show the world what you can do in your programming environment of choice.

[0]: https://omarchy.org/
[1]: https://www.lazyvim.org/
[2]: https://github.com/folke/lazy.nvim
[3]: https://github.com/nikitabobko/AeroSpace
[4]: https://ghostty.org/
[5]: https://github.com/tmux/tmux/wiki
[6]: https://neovim.io/
[7]: https://community.folivora.ai/t/bringing-omarchy-to-macos-using-the-majestic-btt/44881
[8]: https://blog.codinghorror.com/douchebaggery/
