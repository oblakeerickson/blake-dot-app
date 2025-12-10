---
layout: post
title:  "Angular Form Validation"
date:   2015-07-09 01:00:00 -0600
---

Inside of [Todo App][1] there is an input field for adding new Todo items to the
list. The problem I have right now is that there is no JavaScript validation on
the input and if I accidently try and submit an empty Todo I will get a 400
error from the server, but the user will not be notified. This post will walk you
through the steps to take to add some validation to your form with Angular.

Here is the current html for the form:

```
<form novalidate class="form-inline">
     <div class="form-group">
         <input type="text" 
                 class="form-control" 
                 ng-model="name"
                 focus-element />
     </div>
     <input class="btn btn-default" type="submit" ng-click="add(name)" value="Add" />
</form>  
```

There are several things that need to be addressed for validation to work. The
first thing we need to do is name our form.

```
<form name="itemForm" class="form-inline" novalidate>
```

We named the form `itemForm` and notice that even though we are adding
validation to the form it still has the `novalidate` attribute (kinda confusing
right???). `novalidate` means that we are turning off the built in html5
validation which produces these weird popups that I don't think look all that
great.

The next thing that we need to do is name our input field and add the
`required` attribute. We are naming the input field so that the required
attribute will work.

```
<input type="text" 
       class="form-control"
       name="name"
       ng-model="name"
       required
       focus-element /> 
```

*Even though it takes up more lines I like to line up my attributes vertically
rather than having them all bunched up on one line. I just feel like they are
harder to read and harder to catch errors if they aren't lined up vertically.*

Now let's take a look at the submit button. The problem that we are trying to
solve right now is that the user is allowed to submit an empty todo item. To
keep this from happening we are going to disable the submit button if the input
is empty. To conditionally disable the submit button we will add the
`ng-disabled` attribute to the submit button.

```
<input class="btn btn-default" 
       type="submit" 
       ng-click="add(name)" 
       value="Add"
       ng-disabled="itemForm.$invalid" />
```

Notice that inside of the `ng-disabled` attribute we are referencing the name of
our form `itemForm` and seeing if it is invalid (this is why we needed to name
our form).

And that is actually all that we need to do to make sure the user can't submit
an empty Todo item. There are many other things that we should validate, like
the length of the input, but we will tackle those later.

[1]: https://tdapp.azurewebsites.net
