---
layout: post
title: "Lithium Advanced Setup"
date: 2013-04-11 01:00:00 -0600
---

So in the process if getting familiar with Lithium PHP I've probably installed it like 30 times by now and finally realized the need to store the actual lithium library files in a single location on your computer rather than having lithium installed in every single project folder you start.

I realized this was a problem when I was trying to use git while working on a project between two different computers and whenever I would do a git pull it would break the application and I couldn't even get it to run.

So, if you have already started working on a project and you have the lithium core inside of your project folder already, this is how you can remedy the situation:

```
cd /usr/local/lib
git clone https://github.com/UnionOfRAD/lithium.git
```

Now change into your projects webroot folder. It should be something like this:

```
cd /var/www/my_app
```

or on OS X:

```
cd /Library/WebServer/Documents/my_app
```

Now login in to your github account online and create a new repository with the same name as your project folder. Once that is done you can run the following commands:

```
git remote rm origin
git init
git rm -r library
git add .
git commit -m "removed lithium library folder"
git remote add git remote add origin https://github.com/username/my_app.git
git push origin master
```

Now your app is currently broken because we need to fix the location of your library folder.

Open up my_app/app/config/bootstrap/libraries.php and change the LITHIUM_LIBRARY_PATH line to be:

```
define('LITHIUM_LIBRARY_PATH', dirname('/usr/local/lib/lithium'));
```

Now our app should be working again. Browse to:

```
http://localhost/my_app
```

and you should see your app working just like before.

Now apply your changes

```
git add .
git commit -m "fixed location of lithium library"
git push origin master
```

### New Project setup

If you want to create another lithium project and you already have the lithium library in /usr/local/lib/lithium you don't have to do the git submodule any more to get the new app to work.

So, to set up a new lithium project, simply type:

```
cd /var/www/
sudo git clone https://github.com/UnionOfRAD/framework.git new_app
sudo vim /var/www/new_app/app/config/bootstrap/libraries.php
```

and change the LITHIUM_LIBRARY_PATH line to:

```
define('LITHIUM_LIBRARY_PATH', dirname('/usr/local/lib/lithium'));
```

and when you browse to:

```
http://localhost/new_app
```

The default lithium page should be displayed.

### Resources

 - [Advanced Setup](https://web.archive.org/web/20130731124510/http://lithify.me/docs/manual/getting-started/installation.wiki)
 - [Recommended way for me to use git in my lithium project](https://web.archive.org/web/20130731124510/http://stackoverflow.com/questions/7338892/what-is-the-recommended-way-for-me-to-use-git-in-my-lithium-project)

