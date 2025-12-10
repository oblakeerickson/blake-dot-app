---
layout: post
title:  "Ember CLI - TodoMVC Tutorial"
date:   2014-06-17 01:00:00 -0600
---

**Update:** This version was written for ember-cli version 0.0.37. Please read
my [updated tutorial for ember-cli version
0.0.47]({% post_url 2014-10-03-ember-cli-todo-mvc-tutorial-0-0-47 %}).

Welcome to Ember CLI! This guide mirrors what is in the official ember.js
getting started guide, but walks you through doing it with Ember CLI. Some
things will be different than the guide, which is why I wrote this guide to help
you through those differences and hopefully you won't struggle as much as I did.

I do recommend reading the getting started guide first since I'm going to leave
out some of the details that it covers more throughly.

## Getting Started

We will need to install ember-cli. Here are the most basic steps for getting it installed on your system for more details please see the [official website](http://iamstef.net/ember-cli/).

At your terminal type:

    npm install -g ember-cli

And now install Bower:

    npm install -g bower

Now navigate to where you want to place your project code and create a new ember app:

    ember new todos

Now start the server:

    cd todos
    ember server

Navigate to `http://localhost:4200` to see your new app in action.

## Planning The Application

There are no differences in this section

## Creating a Static Mockup

Replace the text inside of `app/templates/application.hbs` with the following:

```
<section id="todoapp">
  <header id="header">
    <h1>todos</h1>
    <input type="text" id="new-todo" placeholder="What needs to be done?" />
  </header>

  <section id="main">
    <ul id="todo-list">
      <li class="completed">
        <input type="checkbox" class="toggle">
        <label>Learn Ember.js</label><button class="destroy"></button>
      </li>
      <li>
        <input type="checkbox" class="toggle">
        <label>...</label><button class="destroy"></button>
      </li>
      <li>
        <input type="checkbox" class="toggle">
        <label>Profit!</label><button class="destroy"></button>
      </li>
    </ul>

    <input type="checkbox" id="toggle-all">
  </section>

  <footer id="footer">
    <span id="todo-count">
      <strong>2</strong> todos left
    </span>
    <ul id="filters">
      <li>
        <a href="all" class="selected">All</a>
      </li>
      <li>
        <a href="active">Active</a>
      </li>
      <li>
        <a href="completed">Completed</a>
      </li>
    </ul>

    <button id="clear-completed">
      Clear completed (1)
    </button>
  </footer>
</section>

<footer id="info">
  <p>Double-click to edit a todo</p>
</footer>
```

Replace the contents of `app/styles/app.css` with this [stylesheet](http://emberjs.com.s3.amazonaws.com/getting-started/style.css).

Inside of the `public/` folder create a new folder called `assets` and place the [`bg.png`](http://emberjs.com.s3.amazonaws.com/getting-started/bg.png) file in that folder.

## Obtaining Ember.js and Dependencies

We've already obtained Ember.js and dependencies! Move on to the next section.

## Adding the First Route and Template

Inside `app/router.js` file add this line to the `Router.map` body:

```
this.resource('todos', { path: '/' });
```

The `app/router.js` file should look like this now:

```javascript
import Ember from 'ember';

var Router = Ember.Router.extend({
  location: TodosENV.locationType
});

Router.map(function() {
  this.resource('todos', { path: '/' });
});

export default Router;
```

Now copy the entire contents of the `app/templates/application.hbs` file into a new file called `app/templates/todos.hbs`.

Then replace the entire contents of the `app/templates/application.hbs` file with:

{% raw %}
```handlebars
{{outlet}}
```
{% endraw %}

Now go back to your web browser and make sure everything still loaded okay.

## Modeling Data

Before we create our model we need to edit `Brocfile.js` so that ember-data will work:

```javascript
app.import({
  development: 'vendor/ember-data/ember-data.js',
  production:  'vendor/ember-data/ember-data.prod.js'
}, {
  'ember-data': [
    'default'
  ]
});
```

Create a file at `js/models/todo.js` and put the following code inside:

```javascript
import DS from 'ember-data';

var Todo = DS.Model.extend({
  title: DS.attr('string'),
  isCompleted: DS.attr('boolean')
});

export default Todo;
```

## Using Fixtures


To enable fixtures create the folder `app/adapters` and then create the file: `app/adapters/application.js` and place the following code inside:

```javascript
import DS from 'ember-data';

export default DS.FixtureAdapter.extend();
```

Now go back to our model `app/models/todo.js` and the fixture to it so that the file now looks like:

```javascript
import DS from 'ember-data';

var Todo = DS.Model.extend({
  title: DS.attr('string'),
  isCompleted: DS.attr('boolean')
});

Todo.reopenClass({
  FIXTURES: [
    {
      id: "1",
      title: 'install ember-cli',
      isCompleted: true
    }, {
      id: "2",
      title: 'install additional dependencies',
      isCompleted: true
    }, {
      id: "3",
      title: 'develop amazing things',
      isCompleted: false
    }
]});

export default Todo;
```

## Displaying Model Data

Create a file called `app/routes/todos.js` and place the following code inside:

```javascript
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    return this.store.find('todo');
  }
});
```

Now we need to add some handlebar code to our `app/templates/todos.hbs` template so that it can dynamically load the contents of our fixture.

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<ul id="todo-list">
  {{ "{{#each" }}}}
    <li>
      <input type="checkbox" class="toggle">
      <label>{{ "{{title" }}}}</label>
      <button class="destroy"></button>
    </li>
  {{ "{{/each" }}}}
</ul>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

## Displaying a Model's Complete State

Update the `<li>` tag in `app/templates/todos.hbs`:

{% raw %}
```html
<!--- ... additional lines truncated for brevity ... -->
<li {{bind-attr class="isCompleted:completed"}}>
  <input type="checkbox" class="toggle">
  <label>{{title}}</label>
  <button class="destroy"></button>
</li>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

## Creating a New Model Instance

At the top of `app/templates/todos.hbs` replace the new todo `<input>` with an `{{ "{{input" }}}}` helper:

{% raw %}
```html
<!--- ... additional lines truncated for brevity ... -->
<h1>todos</h1>
{{input type="text" id="new-todo" placeholder="What needs to be done?"
          value=newTitle action="createTodo"}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

Inside of the `app/controllers/` folder create a new file called: `todos.js` and put the following code inside of it:

{% highlight javascript %}
import Ember from 'ember';

export default Ember.ArrayController.extend({
  actions: {
    createTodo: function() {
      // Get the todo title set by the "New Todo" text field
      var title = this.get('newTitle');
      if (!title.trim()) { return; }

      // Create the new Todo Model
      var todo = this.store.createRecord('todo', {
        title: title,
        isCompleted: false
      });

      // Clear the "New Todo" text field
      this.set('newTitle', '');

      // Save the new model
      todo.save();
    }
  }
});
{% endhighlight %}

## Marking a Model as Complete or Incomplete

Inside the `app/templates/todos.hbs` template replace the `<input>` tag for the checkbox with:

{% raw %}
```handlebars
{{#each}}
  <li {{bind-attr class="isCompleted:completed"}}>
    {{input type="checkbox" checked=isCompleted class="toggle"}}
    <label>{{title}}</label>
    <button class="destroy"></button>
  </li>
{{/each}}
```
{% endraw %}

Inside of the `app/controllers/` folder create a new file called: `todo.js`. And place the following code inside:

```javascript
import Ember from 'ember';

export default Ember.ObjectController.extend({
  isCompleted: function(key, value){
    var model = this.get('model');

    if (value === undefined) {
      // property being used as a getter
      return model.get('isCompleted');
    } else {
      // property being used as a setter
      model.set('isCompleted', value);
      model.save();
      return value;
    }
  }.property('model.isCompleted')
});
```
## Displaying the Number of Incomplete Todos

Update the static count inside the `todo-count` span in the `app/templates/todos.hbs` template:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<span id="todo-count">
  <strong>{{remaining}}</strong> {{inflection}} left
</span>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

Add this to the `app/controllers/todos.js` file:

```javascript
// ... additional lines truncated for brevity ...
actions: {
// ... additional lines truncated for brevity ...
},

remaining: function() {
  return this.filterBy('isCompleted', false).get('length');
}.property('@each.isCompleted'),

inflection: function() {
  var remaining = this.get('remaining');
  return remaining === 1 ? 'todo' : 'todos';
}.property('remaining')
// ... additional lines truncated for brevity ...
```

## Toggling between Showing and Editing States

Update `app/templates/todos.hbs` with the following code to enable toggling in and out of edit mode:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
{{#each itemController="todo"}}
  <li {{bind-attr class="isCompleted:completed isEditing:editing"}}>
    {{#if isEditing}}
      <input class="edit">
    {{else}}
      {{input type="checkbox" checked=isCompleted class="toggle"}}
      <label {{action "editTodo" on="doubleClick"}}>{{title}}</label>
      <button class="destroy"></button>
    {{/if}}
  </li>
{{/each}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

And then update our `app/controllers/todo.js` controller:

```javascript
// ... additional lines truncated for brevity ...
export default Ember.ObjectController.extend({
  actions: {
    editTodo: function() {
      this.set('isEditing', true);
    }
  },

  isEditing: false,

  isCompleted: function(key, value){
// ... additional lines truncated for brevity ...
```

You can now double-click a todo to edit it.

## Accepting Edits

In `app/templates/todos.hbs` change out the static input tag under if editing:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
{{#if isEditing}}
  {{input class="edit" value=title focus-out="acceptChanges" insert-newline="acceptChanges" autofocus="autofocus"}}
{{else}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

## Deleting a Model

In `app/templates/todos.hbs` update the delete button:

{% raw %}
```handlbars
<!--- ... additional lines truncated for brevity ... -->
<button {{action "removeTodo"}} class="destroy"></button>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/controllers/todo.js` add the `removeTodo` action:

```javascript
// ... additional lines truncated for brevity ...
actions: {
  editTodo: function() {
    this.set('isEditing', true);
  },
  acceptChanges: function() {
    this.set('isEditing', false);

    if (Ember.isEmpty(this.get('model.title'))) {
      this.send('removeTodo');
    } else {
      this.get('model').save();
    }
  },
  removeTodo: function() {
    var todo = this.get('model');
    todo.deleteRecord();
    todo.save();
  }
},
// ... additional lines truncated for brevity ...
```


Now you can delete todos.

## Adding Child Routes

Inside of `app/templates/todos.hbs` move the entire contents of `<ul id="todo-list"` section into a new template called: `app/templates/todos/index.hbs`.

Within `app/templates/todos.hbs` place a Handlebars `{{ "{{outlet" }}}}` helper where the `<ul>` was previously:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<section id="main">
  {{outlet}}

  <input type="checkbox" id="toggle-all">
</section>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/router.js` change the `todos` mapping with an additional empty function parameter so it can accept child routes:

```javascript
Router.map(function() {
  this.resource('todos', { path: '/' }, function() {
    // additional child routes will go here later
  });
});
```

Create a new folder called `todos` inside of the `app/routes/` directory.

Create a new file called `index.js` inside of the `app/routes/todos/` directory and add the following code:

```javascript
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    return this.modelFor('todos');
  }
});
```

## Transitioning to Show Only Incomplete Todos

In `app/templates/todos.hbs` convert the `<a>` tag for 'Active' todos into a Handlebars `{{link-to}}` helper:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<li>
  <a href="all">All</a>
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  <a href="completed">Completed</a>
</li>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/router.js` update the router to recognize this new path:

```javascript
// ... additional lines truncated for brevity ...
Router.map(function() {
  this.resource('todos', { path: '/' }, function() {
    this.route('active');
  });
});
// ... additional lines truncated for brevity ...
```

In `app/routes/todos/active.js` implement a matching route:

```javascript
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    return this.store.filter('todo', function(todo) {
      return !todo.get('isCompleted');
    });
  },
  renderTemplate: function(controller) {
    this.render('todos/index', { controller: controller} );
  }
});
```

## Transitioning to Show Only Complete Todos

In `app/templates/todos.hbs` convert the `<a>` tag for 'Completed' todos into a Handlebars `{{link-to}}` helper:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<li>
  <a href="all">All</a>
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  {{#link-to "todos.completed" activeClass="selected"}}Completed{{/link-to}}
</li>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/router.js` update the router to recognize this new path:

```javascript
Router.map(function() {
  this.resource('todos', { path: '/' }, function() {
    this.route('active');
    this.route('completed');
  });
});
```

In `app/routes/todos/completed.js` implement a matching route:

```javascript
import Ember from 'ember';

export default Ember.Route.extend({
  model: function() {
    return this.store.filter('todo', function(todo) {
      return todo.get('isCompleted');
    });
  },
  renderTemplate: function(controller) {
    this.render('todos/index', {controller: controller});
  }
});
```

## Transitioning back to Show All Todos

In `app/templates/todos.hbs` convert the `<a>` tag for 'All' todos into a Handlebars `{{ "{{link-to" }}}}` helper:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<li>
  {{#link-to "todos.index" activeClass="selected"}}All{{/link-to}}
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  {{#link-to "todos.completed" activeClass="selected"}}Completed{{/link-to}}
</li>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

## Displaying a Button to Remove All Completed Todos

In `app/templates/todos.hbs` update the static `<button>` for clearing all completed todos:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
{{#if hasCompleted}}
  <button id="clear-completed" {{action "clearCompleted"}}>
    Clear completed ({{completed}})
  </button>
{{/if}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/controllers/todos.js` implement the matching properties and a method that will clear completed todos and persist these changes when the button is clicked:

```javascript
import Ember from 'ember';

export default Ember.ArrayController.extend({
  actions: {
    clearCompleted: function() {
      var completed = this.filterBy('isCompleted', true);
      completed.invoke('deleteRecord');
      completed.invoke('save');
    },
    // ... additional lines truncated for brevity ...
  },
  hasCompleted: function() {
    return this.get('completed') > 0;
  }.property('completed'),

  completed: function() {
    return this.filterBy('isCompleted', true).get('length');
  }.property('@each.isCompleted'),
  // ... additional lines truncated for brevity ...
```

## Indicating When All Todos Are Complete

In `app/templates/todos.hbs` replace the static checkbox `<input>` with an `{{ "{{input" }}}}`:

{% raw %}
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<section id="main">
  {{outlet}}
  {{input type="checkbox" id="toggle-all" checked=allAreDone}}
</section>
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/controllers/todos.js` implement the matching `allAreDone` property:

```javascript
// ... additional lines truncated for brevity ...
allAreDone: function(key, value) {
  return !!this.get('length') && this.isEvery('isCompleted');
}.property('@each.isCompleted')
// ... additional lines truncated for brevity ...
```

## Toggling All Todos Between Complete and Incomplete

Update the `allAreDone` property in `app/controllers/todos.js` to handle both getting and setting behavior:

```javascript
// ... additional lines truncated for brevity ...
allAreDone: function(key, value) {
  if (value === undefined) {
    return !!this.get('length') && this.everyProperty('isCompleted', true);
  } else {
    this.setEach('isCompleted', value);
    this.invoke('save');
    return value;
  }
}.property('@each.isCompleted')
// ... additional lines truncated for brevity ...
```

## Replacing the Fixture Adapter with Another Adapter

I couldn't figure out how to get this to work with ember-cli, but I will be writing another post that talks about how to connect to a Rails backend for data persistance.

## Resources

These apps helped me along when I got stuck while writing this tutorial:

* [WMeldon: ember-cli-todos](https://github.com/WMeldon/ember-cli-todos)
* [javierjulio: ember-cli-todomvc](https://github.com/javierjulio/ember-cli-todomvc)
* [yhagio: ember-todo](https://github.com/yhagio/ember-todo)
