---
layout: post
title:  "Blocking Referral Spam With NGINX"
date:   2015-07-05 01:00:00 -0600
---

Referral spam will mess up your website analytics by making it look like you
have more traffic than you really do. Referral spam will also tax your webserver
which is something you definitely don't want. If you are using NGINX as your
webserver this post will show you how to block these spammy domains.

### Edit nginx.conf

The first thing we need to do is edit the `/etc/nginx/nginx.conf file`. Inside
of the `http` block add ([source][2]):

```
##
# Referer spam
##

map $http_referer $bad_referer {
    default 0;
    include /etc/nginx/bad_referer.map;
}
```

Notice what we are using the [`map`][1] command. This allows us to make a new
variable($bad_referer) based on values stored in a text file(bad_referer.map).

The main reason why we are using `map` is because we have a long list of referer
spam domains and I don't want to edit one really long string because they can be
hard to maintain and make the config file look messy.

### Create Referer Spam List

Create a new file in the nginx root directory ('/etc/nginx') called
'bad_referer.map':

```
"~*floating-share-buttons.com" 1;
"~*event-tracking.com" 1;
"~*free-social-buttons.com" 1;
"~*100dollars-seo.com" 1;
"~*buttons-for-website.com" 1;
"~*videos-for-your-business.com" 1;
"~*get-free-traffic-now.com" 1;
"~*success-seo.com" 1;
"~*trafficmonetize.org" 1;
"~*4webmasters.org" 1;
"~*webmonetizer.net" 1;
"~*sitevaluation.org" 1;
"~*dailyrank.net" 1;
"~*rightrelevance.com" 1;
"~*best-seo-offer.com" 1;
"~*semaltmedia.com" 1;
```

The `~*` before each domain means case-insensitive matching. The `1` will be
assigned `$bad_referer` variable so that it will evaluate to true. 

[**NOTE:**][3] The `map` command can only be used inside of the `http` block. 

### Check For Bad Referrer

Now open up `/etc/nginx/sites_available/default` and add the following code to
the `server` block:

```
##
# Referrer exclusions
##

if ($bad_referer) {
    return 444;
}
```

We are using ['444'][4] instead of '403' so that the connection closes immediately
and no information is returned to the spammer. It also will use less server
resources.

**NOTE:** The `if` statement can't be used inside of the `http` block.

### Verify

Before we restart NGINX let's verify that our config file is good by typing in
the following command in the console:

```
nginx -t
```

If the test is successful go ahead and restart NGINX:

```
service nginx restart
```

Now to test that blocking is actually working we can run the following curl
command:

```
curl -e "http://www.success-seo.com" "http://blaketv.com"
```

Which should return a message like:

```
curl: (52) Empty reply from server
```

**Update Jul 6, 2015**: Thanks to [@JF0LKINS][5], I updated this post (and my
config) so that NGINX would  return '444' instead of '403'.

[1]: http://nginx.org/en/docs/http/ngx_http_map_module.html
[2]: http://serverfault.com/a/646344/150695
[3]: http://openresty.org/download/agentzh-nginx-tutorials-en.html 
[4]: http://httpstatus.es/444
[5]: https://twitter.com/JF0LKINS/status/617724077373927424
