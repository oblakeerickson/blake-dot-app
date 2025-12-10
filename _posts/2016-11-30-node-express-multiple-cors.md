---
layout: post
title:  "How to add multiple CORS endpoints in express "
date:   2016-11-30 01:00:00 -0600
---

For [SkillSift](https://www.skillsift.com) I currently have two separate front
end single page applications that have their own urls. One is for the actual app
itself and the other is for the sysadmin app. They both need to talk to the same
API though.

Originally I was doing something like this:

```
res.header('Access-Control-Allow-Origin', 'http://localhost:3001');
res.header('Access-Control-Allow-Origin', 'http://localhost:3002');
```

but the second line just overrides the first line so you can no longer access the api from 'http://localhost:3001'.

To be able to have multiple CORS origins you can do something like:

```
var cors = function(req, res, next) {
  var whitelist = [
    'http://localhost:3001',
    'http://localhost:3002',
  ];
  var origin = req.headers.origin;
  if (whitelist.indexOf(origin) > -1) {
    res.setHeader('Access-Control-Allow-Origin', origin);
  }
  res.setHeader('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE');
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type,Authorization');
  next();
}
app.use(cors);
```

In the above code we have created an array of approved origins. And if the current origin is in the array then we will set the 'Access-Control-Allow-Origin' just for that origin on this api request.

Also as a side note I'm not really sure what the difference is between `res.header` and `res.setHeader`, but since there is actually documentation on [`res.setHeader`](https://nodejs.org/api/http.html#http_response_setheader_name_value) I'm going to use that.
