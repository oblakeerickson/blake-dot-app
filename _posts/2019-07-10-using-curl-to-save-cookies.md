---
layout: post
title: "Using cURL to Save Cookies"
date: 2019-07-10 01:00:00 -0600
---

Just for fun I want to automatically track if I go to the gym or not. Every time
I go to Golds Gym I have to scan my card that I keep on my key chain so there is
an electronic record of me going to the gym or not. I did not know about this
when I signed up, but Golds Gym does have a [crappy website][2] for managing your
membership and on there you can see a record of every time you have checked into
the gym.

The problem I have with this website is that they don't have an API and it
mostly requires javascript to use it. This makes automatically fetching the data
I need very tricky. Using Firefox's developer tools you can inspect the http
requests and copy them as cURL so that you can kind of reverse engineer how to
authenticate and fetch data.

This works pretty well and I was able to get everything I needed from the
command line using cURL commands, but unfortunatley it only worked for the
lifetime of the session cookie. Even though I have worked with web technology
for many years I actually haven't done a whole lot with cookies. The copy as
cURL command from Firefox will actually copy over all of the cookies into the
cURL request, but that wasn't exactly what I was after. Through some digging
around I found a [great resource on cURL][1] that mentions how to save and
retreive cookies from a text file.

To save a cookie you can use the `-c` flag followed by the name of the cookie
file you want to save. Here is an example:

``` text
curl -c cookie.txt https://example.com?creds=asdf
```

If you then want to use those cookies you can use the `-b` flag like this:

``` text
curl -b cookie.txt https://example.com/data
```

So now I can run one cURL command to authenticate with my username and password
which will save a session token in my cookie file. And then I can run another
cURL command using the cookie file to fetch the data I'm after. Pretty cool.

Now my next steps are to do this all in ruby. After that I'm hoping I can add
this to my private Discourse instance somehow so that I can be awarded a custom
gym badge every day I go or for going so many days in a row.

[1]: https://ec.haxx.se/http-cookies.html
[2]: https://mico.myiclubonline.com/iclub/members/signin.htm
