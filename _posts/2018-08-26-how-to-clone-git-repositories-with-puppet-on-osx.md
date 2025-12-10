---
layout: post
title: "How to Clone Git Repositores with Puppet on OS X"
date: 2018-08-26 06:00:00
---

I'm currently in the process of puppetizing my macOS based laptop, but I'm
noticing some external modules like [vcsrepo][vcs] don't have OS X support.

To clone git repositories using puppet on OS X I'm doing:

```
exec { 'git clone git@github.com:org/repo.git /full-path/repo':
  path    => '/usr/local/bin',
  user    => 'blake'
  creates => '/full-path/repo'
}
```

Which seems to be getting the job done.

[vcs]: https://blog.blakeerickson.com/how-to-clone-git-repositories-with-puppet
