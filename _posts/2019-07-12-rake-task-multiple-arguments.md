---
layout: post
title: "Rake Task with an Arbitrary Amount of Arguments"
date: 2019-07-12 01:00:00 -0600
---

I'm currently working on a rake task where I need to pass in an arbitrary amount
of values. I couldn't even remember at first how to even pass in arguments to a
rake task, so let's cover that first.

For this example we are going to create a file called `raketask.rb` inside of an
empty directory. And inside of that file we can create our first task like so:

``` ruby
desc "A sample task"
task :print_hello do
  puts "hello"
end
```

Once you save and close the file we can run `rake -T` and it will print out a
list of tasks that is knows about:

``` text
rake print_hello      # A sample task
```

And we can call this task with the following command:

``` text
rake print_hello
hello
```

Now let's make another task with an argument:

``` ruby
desc "Say hi"
task :say_hello, [:name] do |t, args|
  puts "Hello #{args.name}"
end
```

If we run `rake -T` again:

``` text
rake print_hello      # A sample task
rake say_hello[name]  # Say hi
```

Unlike command line bash scripts or even calling a ruby script with multiple
args you can't just separate them by spaces in a rake task like this:

``` text
ruby my-sample-script.rb arg1 arg2 arg3
```

Rake task arguments go inside brackets:

``` text
rake say_hello[blake]
Hello blake
```

Now how do we specify multiple arguments? By specifying each one inside of the
task declaration:

``` ruby
desc "Two args"
task :two_args, [:fname, :lname] do |t, args|
  puts "Hello #{args.fname} #{args.lname}"
end
```

And you can run it by specifying args in a comma separated list (with no
spaces!):

``` text
rake two_args[blake,erickson]
Hello blake erickson
```

Now onto the tricky part that I'm still not 100% satisfied with, is how do you
pass in an arbitrary amount of arguments to a rake task? For my case I need to
pass in a list of values, but I'm not sure how many there will be.

To do this you will not specify the args like we did before inside of the task
declaration. The problem with this is now it won't show the args when running
`rake -T`. So to handle an arbitrary amount of args you can use the
[`args.extras`][2] method like so:

``` ruby
desc "Arbitrary args, pass in a comma separated list"
task :arbitrary_args do |t, args|
  puts "There are #{args.extras.count} args"
  args.extras.each do |arg|
    puts arg
  end
end
```

Now you can run the arbitrary args command with:

``` text
rake arbitrary_args[banana,apple,orange,mango]
There are 4 args
banana
apple
orange
mango
```

I'm not totally satisfied with specifying an arbitrary amount of
arguments this way, but it does get the job done. Hopefully this helps you in
your [rake][1] task adventures.

[1]: https://martinfowler.com/articles/rake.html
[2]: https://stackoverflow.com/a/28654953/588458
