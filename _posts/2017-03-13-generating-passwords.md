---
layout: post
title:  "Generating Passwords"
date:   2017-03-13 17:06:12 -0600
---

Every single day I am constantly generating passwords, they could be for some
new account I'm signing up for or just because I need to assign a password to a
new database I'm setting up. So how do I generate these passwords?

Since I live in the browser, I have a bookmark to this page:

https://www.random.org/passwords/?num=1&len=24&format=html&rnd=new

but, lately I feel like that is still too much frinction to generate a password.

Since I also live in the terminal I created a little ruby/shell script that
generates a random password and adds it to my clipboard.

Now in any open terminal that I have I can just type:

```
pass
```

and a new password is instantly in my clipboard.


Here is the code for my ruby file which generates the random password:


```ruby
require 'securerandom'

class Password

  def self.generate
    SecureRandom.hex
  end

end

puts Password.generate
```

and here is the code for my shell script which is located at
`/usr/local/bin/pass` that adds the password to my clipboard:

```
#!/bin/bash
source ~/.bash_profile
source ~/.bashrc

ruby ~/code/pass/pass.rb | xclip -sel c
```

For most of these passwords I generate I don't use a password manager at all and
just rely on the browser to remember the password. Worst case if I lose the
password I will just do a password reset and have a link emailed to me to
generate a new password.
