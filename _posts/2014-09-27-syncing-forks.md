---
layout: post
title:  "Syncing Forks"
date:   2014-09-27 01:00:00 -0600
---

If you start working on an open source project that you don't own you will need to create a fork of it so that the code you are working on lives inside of your repo. You then create a feature branch, make your changes, commit them, and then create a pull request.

Once they merge in your pull request and maybe some other peoples pull requests your forked repo is going to be out of sync with the main project repo. Because they are out of sync you don't want to create another feature branch just yet if you want to make some more changes. What you want to do is sync your fork with the main project repository. This is how you do it:

First thing you are going to want to is configure another repository that you can push to. When you run `git push origin feature-branch` you are pushing to your forked repo on GitHub. 'origin' is the name of this location. To configure another repo to push to run this command:

```
git remote add upstream https://github.com/original_owner/original_repository.git
```

Now you have two locations you can push to: 'origin' and 'upstream'. You can name this whatever you want.

Now that we have our upstream repository configured we can sync our fork. Make sure you are not in your feature branch any more:

```
git checkout master
```

Now you can get the latest code from the main repository:

```
git fetch upstream
```

Now that we have the latest code on our local computer we just need to merge them:

```
git merge upstream/master
```

And that's it. Good luck on your next pull request.

Resources - GitHub has published two great articles on how to sync forks. You should refer to them if you need any more assistance:

- [https://help.github.com/articles/syncing-a-fork](https://help.github.com/articles/syncing-a-fork)
- [https://help.github.com/articles/configuring-a-remote-for-a-fork](https://help.github.com/articles/syncing-a-fork)
