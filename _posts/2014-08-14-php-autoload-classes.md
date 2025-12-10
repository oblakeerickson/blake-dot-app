---
layout: post
title:  "PHP Autoload Classes"
date:   2014-08-14 01:00:00 -0600
---

I've been working for awhile now to clean up a legacy PHP application by breaking up extremely large php files into separate much smaller class files. While the code base is becoming much cleaner and easier to manage its is full of require statements. Personally I don't think require statements are necessarily a bad thing, but it just becomes another things to manage and potentially something that can break.

I've been making great progress on cleaning up our codebase, but I wasn't really sure about some of the best practices in PHP when building a framework so I purchased "[Modernizing Legacy Applications in PHP](https://leanpub.com/mlaphp)" which has been extremely helpful. One of the first things it talks about is autoloading.

To eliminate all of these `require` statements you can call an autoloader method as one of the first things your app runs. Be sure to use [`spl_autoload_register`](http://php.net/manual/en/function.spl-autoload-register.php) and not the old __autoload function.

I'm actually autoloading two different directories. One is a directory called `app` and the other is a directory in `lib/framework`. I put my autoloader inside of `lib/framework` along with my other code like my model, controller, and view classes that I extend. The problem that I had was that inside of my app directly I also have my assets folder and I also have a templates directory which contain mostly html code but are not class files. Anyways I needed to exclude my `app/assets` directory and my `app/templates` directory inside of my autoloader. To exclude my `app/assets` directly I simply check to make sure the file ends with a php extention before requiring it. The problem is that this method would still include my `app/templates` files because they end in `.php`. So to exclude this directory I simply check to see if the path string contains 'templates' and if it does I don't require the php file.

Here is my autoloader file that I'm calling from `setup.php`:

```
<?php
namespace Framework;

class Autoloader
{
    public function loadApp($class)
    {
        $dir = __DIR__ . '/../../app';
        $this->load($class, $dir);
    }

    public function loadFramework($class)
    {
        $dir = __DIR__ . '/..';
        $this->load($class, $dir);
    }

    // private

    private function load($class, $dir)
    {
        // strip off any leading namespace separator from PHP 5.3
        $class = ltrim($class, '\\');

        // the eventual file path
        $subpath = '';

        // is there a PHP 5.3 namespace separator?
        $pos = strrpos($class, '\\');
        if ($pos !== false) {
            // convert namespace separators to directory separators
            $ns = substr($class, 0, $pos);
            $subpath = str_replace('\\', DIRECTORY_SEPARATOR, $ns)
                     . DIRECTORY_SEPARATOR;
            // remove the namespace portion from the final class name portion
            $class = substr($class, $pos + 1);
        }

        // convert underscores in the class name to directory separators
        $subpath .= str_replace('_', DIRECTORY_SEPARATOR, $class);

        // previx with the central directory location and suffix with .php,
        // then require it.
        $file = $dir . DIRECTORY_SEPARATOR . $subpath . '.php';
        if (is_file($file)) {
            if (strpos($file, 'Templates') !== false) {
                // skip
            } else {
                require $file;
            }
        }
    }
}
```

And here is my `lib/setup.php` file:

```
<?php
require_once __DIR__ . '/framework/autoloader.php';

$autoloader = new \Framework\Autoloader();

spl_autoload_register(array($autoloader, 'loadFramework'));
spl_autoload_register(array($autoloader, 'loadApp'));
```
