---
layout: post
title:  "Seed Data For Tests"
date:   2014-09-01 01:00:00 -0600
---

A couple of days ago I got really excited about working on the discourse_api that I just jumped right in and started working on a feature that I wanted. I got even more excited as I figured out how things works and was able to get the results that I wanted. That excitement soon ended when I ran the tests for the first time and realized that everything blew up in my face.

I do think that it is good to ride a wave of excitement if you have one, but I think before starting to work on any project you should start by running the tests. The tests I don't think are entirely broken but to get them to pass you will have to have a very specific environment set up that isn't really documented anywhere.

So, my goal, before I start writing any more features for the discourse_api is to fix the test suite and document the process so that anybody can quickly run the tests.

One of the things that I need to do is [make sure that there is good seed data for the tests to run](https://meta.discourse.org/t/discourse-seed-data-for-discourse-api-tests/19507). I'm not really sure what the best route is for this though. One method is to run a db migration for test data on the discourse database and the other method would be to make sure the disource_api had an admin api key and have it generate all the seed data. Even though the discourse_api depends on discourse I feel like they need to be as decoupled as possible from each other.
