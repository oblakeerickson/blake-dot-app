---
layout: post
title: "The Best Way to Learn Lithium"
date: 2013-04-13 01:00:00 -0600
---

I was introduced to Lithium PHP last week and since then I've been learning as much as I can about the framework.

However there comes a point when the documentation and tutorials can only get you so far. And if you really want to master something new you need to write real applications with it.

So after just a few hours of coding I came out with the first version of DailyWeight.net. It's a simple app that is far from complete, but is certainly usable. Currently you can sign up for an account, login, logout, enter your current weight for a specific day, and see a list of each of the days where you have tracked your weight.

The entire goal of making this app was to not only learn the basics of Lithium, but learn some of the advanced things it can do, as well as get me really familiar with the framework so that I can contribute to the project.

It's hard to get stuck while following tutorials. The real learning comes when you stretch yourself and attempt to make something that doesn't exist yet. Here are some of the things I learned while making dailyweight.net:
Things I learned:

    How to add validations to your model.
    How to create custom validations (ex: checking the db for an already registered username).
    How to only save certain elements from a form in the database (ex: you don't want to save the password confirmation).

Things I'm going to work on next

    Encrypt and Sign Cookies. Right now I'm just using session variables, but I already know that will be an issue as soon as I add a second server.
    Error Handling. A better solution than writing try/catch blocks.
    Unit Testing! Ya ya I know you should be writing tests before you begin your development, but that's the exact reason why I'm making this app now, so that the next app I make I can do TDD.
    Flash messages.
    And many more app enhancements like being able to chart your progress, set a goal weight, and before and after photos.

I already have an idea for the next app I'm going to make and as I continue to learn more about php and Lithium all the pieces for it are coming together nicely in my head. I'm sure I'll start working on it soon.

What app are you going to make to learn Lithium?
