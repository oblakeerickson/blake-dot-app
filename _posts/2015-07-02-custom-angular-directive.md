---
layout: post
title:  "How To Make A Custom Angular Directive"
date:   2015-07-02 01:00:00 -0600
---

If you have a form in your web application chances are you are going to need to
add a behavior to one of the input fields. This post will show you how to build
your very own angular directive.

One use case for a custom Angular directive that I use is to automatically set
the mouse focus to the first input field when a page loads.

Here is an example of an input element:

```
<input type="text" 
       class="form-control" 
       ng-model="name" />
```

From the above code you can see that we just have a simple text input with an
ng-model attribute of name. The ng-model doesn't really matter in this example
though. What we want to do is write some Javascript that will run every time the
page is loaded and put the focus on this input. Here is the JavaScript that will
put the focus on the input element:

```
element[0].focus();
```

But where are we supposed to put this single line of code and how is it going to
know what `element` is? This is where Angular directives come in. Let's create
one:

```
app.directive('focusElement', ['$timeout', function ($timeout) {
    return {
        restrict: 'A',
        link: function ($scope, element, attrs) {
            $timeout(function () {
                element[0].focus();
            });
        }
    }
}]);
```

1. There already is a module named `app` declared and so we can add a directive to it
by specifying `app.directive`. 
2. Give the directive a name like 'focusElement' (notice that the name is
camelCased). 
3. Pass in any depencies that we will need. In this case we will be using
`$timeout`. 
4. Add a `return` statement that we will wrap everything into. 
5. Add a `restrict` statement. Directives can be used in several different ways
and we want to restrict our directive to only be used as an attribute, so we
will use the letter `A`.
6. Specify a `link` statement. This is where the magic happens. Notice
that we are passing in 3 things into our link function: `$scope`, `element`, and
`attrs`. The `element` that we are passing in is going to contain data about any
element we add this directive to. 
7. Write the actual code. We are going to wrap the `focus()` method in a `$timeout` so that
the focus will happen after Angular has finished loading.

The last thing we need to do is return back to our partial where the `input`
field is and add our new directive to it:

```
<input type="text" 
       class="form-control" 
       ng-model="name"
       focus-element />
```

Notice that we used `focus-element` instead of `focusElement`.
