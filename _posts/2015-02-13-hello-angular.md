---
layout: post
title:  "Hello Angular"
date:   2015-02-13 01:00:00 -0600
---

If you are just getting started with Angular I recommend using a site like [jsbin](http://jsbin.com/) so you don't have to setup a local web server or anything else on your first few Angular apps.

Once you get things figured out you will want to get your local dev environment setup so that your Angular app can fetch actual data from a server.

## Your first Angular App

I'm going to be using [jsbin](http://jsbin.com/) if you'd like to follow along. Here is our base html template we have to start out with:

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>JS Bin</title>
</head>
<body>

</body>
</html>
```

The first thing we want to do is include the Angular source:

```
<!DOCTYPE html>
<html>
<head>
<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.3.2/angular.min.js"></script>
<meta charset="utf-8">
<title>JS Bin</title>
</head>
<body>

</body>
</html>
```

Now that we have the Angular source included we need to declare a module. Angular separates sections of your app with modules. Large apps can have multiple modules, but smaller apps usually just have one module declared.

```
<!DOCTYPE html>
<html>
<head>
  <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.3.2/angular.min.js"></script>
  <script>
    var app = angular.module("app", []);
  </script>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body>
</body>
</html>
```

The next thing we need to do is create our model. Models will typically interact with some server backend and fetch JSON, but we are just going to store a string that we can display in our view.

```
<script>
var app = angular.module("app", []);

var model = {
  message: "Hello Angular!"
};
</script>
```

Now we can create a controller that will store our model and can be accessed from our view.

```
<script>
var app = angular.module("app", []);

var model = {
  message: "Hello Angular!"
};

app.controller("AppCtrl", function ($scope) {
  $scope.stuff = model;
});
</script>
```

Now that we have an Angular module, model, and controller setup we can go to our body tag and specify that we want to use the "AppCtrl" controller.

```
<body ng-controller="AppCtrl">
```

And now we can display the message from our model. We access it using the handlebar syntax:

```
<body ng-controller="AppCtrl">
  <h1>{{ "{{stuff.message" }}}}</h1>
</body>
```

At this point our message still doesn't show up on our html page though. We need to do one last step and that is specify the angular module we are using in the html tag.

```
<html ng-app="app">
```

Now our "Hello Angular!" message will show up.

Here is the complete [source](http://jsbin.com/giwide/4/edit?html,output) file:

```
<!DOCTYPE html>
<html ng-app="app">
<head>
  <script src="//ajax.googleapis.com/ajax/libs/angularjs/1.3.2/angular.min.js"></script>
  <script>
    var app = angular.module("app", []);

    var model = {
      message: "Hello World!"
    };

    app.controller("AppCtrl", function ($scope) {
      $scope.stuff = model;
    });
  </script>
  <meta charset="utf-8">
  <title>JS Bin</title>
</head>
<body ng-controller="AppCtrl">
  <h1>{{ "{{stuff.message" }}}}</h1>
</body>
</html>
```
