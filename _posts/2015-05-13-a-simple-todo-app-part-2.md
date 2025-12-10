---
layout: post
title:  "A Simple Todo App - Part 2"
date:   2015-05-13 01:00:00 -0600
---

In [Part 1](/2015/04/20/a-simple-todo-app-part-1/) we built the backend for our
todo app and now we are going to build the frontend in Angular. Let's get that
setup.

## Download Angular and Create Bundle

The first thing we need to is download angular and add it to our C# project. Go
to [https://code.angularjs.org](https://code.angularjs.org) and click on 1.2.2
(yes, I'm using an older version). Download 'angular.js' and put it into your
Scripts folder. You now need to show all files and then select the 'angular.js'
file and click add to project.

Now open up BundleConfig.cs located inside of the `App_Start` folder. At the
bottom of the `RegisterBundles` method add another bundle that we will call
`angular`.

``` 
bundles.Add(new ScriptBundle("~/bundles/angular").Include( 
    "~/Scripts/angular.js")); 
```

Now that we have angular installed we need a place to store the actually
JavaScript application code. Inside of the Scripts folder create a folder called
'app' and create a file inside of that folder called 'app.js'.

Now we need to go back to our 'BundleConfig.js' file and add another bundle we
will call `app`.

``` 
bundles.Add(new ScriptBundle("~/bundles/app").Include(
    "~/Scripts/app/app.js"));
```

## Add Angular to Layout

We still are not quite setup yet we still need to include our bundle into our
layout file. So open up `_Layout.cshtml` which is inside of 'Views/Shared/'. Near
the top inside of the `<head></head>` tags add the following lines below the
other `@Scripts.Render` line:

```
@Scripts.Render("~/bundles/angular")
@Scripts.Render("~/bundles/app")
```

Still inside of `Views/Shared/_Layout.cshtml` modify the `<html>` tag so that it
looks like:

```
<html ng-app="app">
```

This lets angular know that we want to start using it.

## Create Our Angular App and Controller

Now let's open up `Scripts/app/app.js` to start working on the angular part of
our app:

{% highlight javascript %}
var model = {};

var app = angular.module('app', []);

app.controller("ToDoCtrl", function ($scope, $http) {

    $http.get("api/TodoItems").success(function (data) {
        model.items = data;
    });

    $scope.todo = model;

});
{% endhighlight %}

In the above section of code we created an angular module and gave it the name
of 'app'. We then created a controller called "ToDoCtrl" and told it it fetch
data from our api and store it in model.items. We then added model.items to our
`$scope` so that we can access it our view, which we will create next.

## Create Our View 

Now open up `Views/Home/Index.cshtml` and replace the entire contents with:

```
<div class="todoItems" ng-controller="ToDoCtrl">
    <div class="container body-content">
        <div class="page-header">
            <h1>Todo List</h1>
        </div>
        <div class="panel col-md-4">
            <table class="table table-striped">
                <thead>
                    <tr>
                        <th>Description</th>
                    </tr>
                </thead>
                <tbody>
                    <tr ng-repeat="item in todo.items">
                        <td>{{item.Name}}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</div>
```

The above html code specifies that we are using the "ToDoCtrl" and using an
angular directive called `ng-repeat` to loop through each of the todo items.

## See Our Work

On your Visual Studio tool bar you should be able to hit the green "Continue"
(Play) button and have your app open up in a web browser. You should see your
list of todo items.

## Wrap Up

This concludes Part 2 where we used angular to display our todo items. In [Part
3](/2015/05/18/a-simple-todo-app-part-3/)
we will work on being able to create and delete todo items.
