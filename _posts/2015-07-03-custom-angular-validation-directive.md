---
layout: post
title:  "How To Make A Custom Angular Validation Directive"
date:   2015-07-03 01:00:00 -0600
---

There are many built it ways to validate an input field with Angular, but
sometimes you need to validate some non-standard data. This post will walk you
through how to build your own directive to validate an input field.

Below we have a simple input field that is wanting an even number, but we
currently have no way to validate that the user has typed a number that is
actually even. 

```
<input type="text" 
       class="form-control" 
       ng-model="evenNumber"
       placeholder="Even Number" />
```

To be able to validate this input we need to [create an Angular
directive](/2015/07/02/custom-angular-directive/).

```
app.directive('isEven', [function () {
    return {
        require: 'ngModel',
        link: function ($scope, element, attrs, ngModel) {
            element.on('blur change', function () {
                var isEven = function (number) {
                   if (number % 2 == 0) {
                       return true;
                   } else {
                       return false;
                   } 
                }
                
                var number = ngModel.$modelValue || '';
                ngModel.$setValidity('isEven', isEven(number));
            });
        }
    }
}]);
```

There are a couple important things we did in this directive that will allow us
to set the validity. In order to check if the input is valid we need a way to
actually get the value of the input. To get the value of the input we need to
require 'ngModel' and then pass it in as the forth argument on the link function.
We can then access the value with `ngModel.$modelValue`;

Notice that we created an `isEven` function that will return `true` if the
number is even and `false` if it is odd.

The key part to this directive is the `$setValidity` method we have at the end
of our directive.

```
ngModel.$setValidty('isEven', isEven(number));
``` 

The first argument to `$setValidity` is a string known as the
validationErrorKey. The second argument is a boolean value which we are
returning from the isEven function we created.

To use the directive add `is-even` to the input as an attribute:

```
<input type="text" 
       class="form-control" 
       ng-model="evenNumber"
       placeholder="Even Number"
       is-even />
```

Now because the validity is being set you can check if the form is valid before
saving the form. If the number is even the form will be valid and if the number
is odd the form will be invalid.
