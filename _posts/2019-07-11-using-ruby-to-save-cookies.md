---
layout: post
title: "Using Ruby to Save Cookies"
date: 2019-07-11 01:00:00 -0600
---

Like I mentioned in my [previous post][1] about saving cookies with cURL in this
post I'm going to show you how to do it with ruby.

I found [this stackoverflow answer][2] that talks about using [http-cookie][3]
which doesn't look like it has been updated in over 3 years, but it did work
just fine.

I created the [golds_checkin][4] repo to store the ruby code of this project.
Currently it is just an app.rb file, but I will most likely turn it into an
actual ruby gem.

Here is the output of my app.rb file:

``` ruby
require 'yaml'
require 'net/http'
require 'http-cookie'
require 'cgi'

class GoldsCheckin
  def initialize
    @config = YAML.load_file('config.yml')
    @jar = HTTP::CookieJar.new
  end

  def login
    uri = URI('https://mico.myiclubonline.com/iclub/j_spring_security_check')

    Net::HTTP.start(uri.host, uri.port, use_ssl: true) do |http|
      req = Net::HTTP::Post.new uri
      req.form_data = { "j_username": @config['username'], "j_password": @config['password'] }
      res = http.request req
      res.get_fields('Set-Cookie').each do |value|
        @jar.parse(value, req.uri)
      end
    end
  end

  def fetch_checkins
    low_date = CGI::escape(Time.now.strftime("%m/%d/%Y"))
    high_date = CGI::escape(Time.now.strftime("%m/%d/%Y"))
    uri = URI("https://mico.myiclubonline.com/iclub/account/checkInHistory.htm?lowDate=#{low_date}&highDate=#{high_date}")

    Net::HTTP.start(uri.host, uri.port, use_ssl: true) do |http|
      req = Net::HTTP::Get.new(uri)
      req['Cookie'] = HTTP::Cookie.cookie_value(@jar.cookies(uri))
      res = http.request req
      res.body
    end
  end


end

golds_checkin = GoldsCheckin.new

golds_checkin.login
puts golds_checkin.fetch_checkins
```

Basically there are two methods, 'login' and 'fetch_checkins'. 'login' reads my
credentials out of a yaml file and makes a POST request wich then sets the
returned cookies into the @jar instance variable so that we can use it for
subsequent requests. Once we are logged in then we can call 'fetch_checkins'
which I have set to only fetch today's date. This call reads from the cookie jar
in order to make an authenticated request.

From these two posts (this one and [yesterdays][1]) you can start to see my
process for making an app. I usually start with just playing around on the
command line. Then I translate all of that knowledge into a simple app.rb file.
From there I think it kind of depends what my end goal is, but then the app.rb
file evolves in some way where it no longer just lives on my local computer, but
gets turned into a ruby gem to be used in another project, or it evovles into a
larger web application.

[1]: https://blog.blakeerickson.com/using-curl-to-save-cookies
[2]: https://stackoverflow.com/a/32868560/588458
[3]: https://github.com/sparklemotion/http-cookie
[4]: https://github.com/oblakeerickson/golds_checkin

