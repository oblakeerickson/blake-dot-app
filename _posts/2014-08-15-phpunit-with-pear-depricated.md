---
layout: post
title:  "PHPUnit with PEAR Deprecated"
date:   2014-08-15 01:00:00 -0600
---

So I installed PHPUnit today with PEAR and apparently that wasn't what I should have done because the [PHPUnit PEAR installing method has been officially deprecated](https://github.com/sebastianbergmann/phpunit/wiki/End-of-Life-for-PEAR-Installation-Method).

If you did what I did and installed PHPUnit with PEAR you can easily uninstall it with:

   pear uninstall phpunit/PHPUnit

And then install it [with PHAR](http://phpunit.de/manual/4.1/en/installation.html):

    wget https://phar.phpunit.de/phpunit.phar
    chmod +x phpunit.phar
    mv phpunit.phar /usr/local/bin/phpunit

You might need to restart your terminal for the `phpunit` command to work.
