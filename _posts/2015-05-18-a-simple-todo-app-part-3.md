---
layout: post
title:  "A Simple Todo App - Part 3"
date:   2015-05-18 01:00:00 -0600
---

In [Part 1](/2015/04/20/a-simple-todo-app-part-1/) we built the backend for our
todo app and in [Part 2](/2015/05/13/a-simple-todo-app-part-2/) we built 
the frontend in Angular. In Part 3 we will add some more functionality like
being able to add and delete todo items. 

## Create The Input Form 

Being able to create a todo item will actually be fairly easy because we already
have the backed finished. We will just need to add an input field and button to
our html view and then write some JavaScript to talk to our backend.

Open up the `Index.cshtml` file and add the following code just below the `<div
class="panel col-md-4">` and before the `<table>` tag:

``` 
<form class="form-inline">
    <input class="form-control" 
           type="text"
           ng-model="name" />
    <input class="btn btn-default" 
           type="submit"
           ng-click="add(name)" 
           value="Add" />
</form>
```

Notice that we added an `ng-model` and an `ng-click` tag. These tags will be
used by Angular to read data from our input field.

## Angular Add Method 
 
Now let's open up the `app.js` file and add some code to the `TodoItemsCtrl`. We
are going to create the `add()` method that we referenced in our view.

Just below the line `$scope.todo = model;` add the following section of code:

```
$scope.add = function (name) {
    $http({
        method: 'POST',
        url: '/api/TodoItems/',
        data: { Name: name }
    })
    .success(function (data) {
        $scope.todo.items.push(data);
        $scope.name = '';
    })
}
```

In the above code we pass in the name from our input field and perform a 'POST'
request to our C# controller. If the request was successful we add the todo item
to our table and then clear the input field.

If you start your debugger again you should now be able to create your own todo
items.

## Create The Delete Method

Now let's work on being able to delete todo items. Let's start with adding a
delete button to each row in our table. Open up `Index.cshtml` again and after
the `<td>` element inside of the `<tr>` tags add the following code:

```
<td><button class="btn btn-xs" ng-click="remove(todo)">Delete</button></td>
```

Notice that we added the `ng-click` attribute that will call the `remove()`
method inside of our controller.

## Angular Remove Method

Back inside of the `app.js` file just below the `$scope.add` block of code add:

```
$scope.remove = function (todo) {
    $http({
        method: 'DELETE',
        url: '/api/TodoItems/' + todo.Id
    })
    .success(function (data) {
        $scope.todo.items.splice($scope.todo.items.indexOf(todo), 1);
    });
}
```

This code will get the id of the todo item we want to delete and then perform a
'DELETE' request to our C# controller. If the result was successful it will then
remove itself from the todo list.

Go ahead and try it out yourself and see if you can delete one of your todo
items.

## Wrap Up

This last article concludes this 3 Part series on how to make a simple todo app
with Angular and .NET. I hope this tutorial was able to help you learn some of
the basics of how Angular can talk to a backend api. If you have any questions
or comments please reach out.

