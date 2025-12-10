---
layout: post
title:  "How to create a Vue.js moment date filter"
date:   2016-12-05 01:00:00 -0600
---

In Vue.js I'm currently working on building a table that lists blog posts and
one of the columns includes the date the blog post was published. The dates
coming back from the server are not formatted so I wanted to hook up a date
filter, this is how I did it inside of my blog post component:


```
var BlogPosts = {
  template: `\
    ...
    <div class="col-md-2">\
      {{p.date_published | YYYYMMDD}}\
    </div>\
    ...
  ',
  data: function() {
    //...
  },
  filters: {
    truncate: function(value) {
      //...
    },
    YYYYMMDD: function(date) {
      return moment(date).format('YYYY-MM-DD');
    }
  },
  methods: {
    //...
  },
  mounted: function() {
    //...
  }
};

```

Apparently filter names can't have `-` in them, so keep that in mind is you
build yours.

Also this filter is tied to my component, but it is something I might want to
use in other components so I might need to move it out into my main app.js file.
