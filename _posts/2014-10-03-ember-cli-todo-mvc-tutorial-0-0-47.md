---
layout: post
title:  "Ember CLI - TodoMVC Tutorial (for v0.0.47)"
date:   2014-10-03 01:00:00 -0600
---

This post will walk you through how to build the Todo MVC app that the [Official Ember Getting Started Guide](http://emberjs.com/guides/getting-started/) walks you through but shows you how to use Ember CLI instead.

Using Ember CLI has many benefits over just linking to ember in your html script tag, here are a few:

- Comes with a built in webserver
- Auto builds your code so you don't have to refresh the browser all the time (there might be a bug in 0.0.47 that is keeping this from working)
- Default folder structure so every project looks the similar
- Can generate model, controller, template, route, and test files for you
- You can write ES6 javascript

Because ember-cli is so helpfull it is going to be part of ember 2.0 so I think it is very beneficial to start getting familiar with it now.

## Getting Started

The first thing we need to do is install Ember CLI. Here are the basic steps for getting it installed on your system. For more details please see the [official website](http://www.ember-cli.com/#getting-started). This guide was written for Ember CLI version 0.0.47. Other versions might work but your mileage may vary. Anyways, back to installing Ember CLI

At your terminal type:

```
npm install -g ember-cli
```

And now install Bower:

```
npm install -g bower
```

Now navigate to where you want to place your project code and create a new ember app:

```
ember new todos
```

Now start the server:

```
cd todos
ember server
```

Navigate to `http://localhost:4200` in your web browser to see your new app in action. I recommend using Chrome or Firefox because they have [Ember Inspector](https://github.com/emberjs/ember-inspector), but also because I feel like those browsers have better tooling for viewing javascript errors.

Inside of your browser you should see simple page that says: "Welcome to Ember.js". On this page right-click and select 'Inspect Element' so that you can see if any javascript errors occur while we are building our app.

I like to leave the server running in my terminal, since it will automatically build any changes you make. So create a new terminal tab/window and stay inside the todos directory so that we can run some ember commands.

## Planning The Application

There are no differences in this section

## Creating a Static Mockup

Replace the text inside of `app/templates/application.hbs` with the following:

```html
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

```javascript
this.resource('todos', { path: '/' });
```

The `app/router.js` file should look like this now:

```javascript
import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
  this.resource('todos', { path: '/' });
});

export default Router;
```

From the terminal type:

```javascript
ember generate route todos
```

This will create a new file for us inside of `app/templates/todos.hbs`. Now copy the entire contents of the `app/templates/application.hbs` file into this new file.

Then replace the entire contents of the `app/templates/application.hbs` file with:

{% raw %}
```handlebars
{{outlet}}
```
{% endraw %}

Now go back to your web browser and make sure everything still loaded okay.

## Modeling Data

From the terminal type:

```
ember generate model todo
```

Now open up `js/models/todo.js` and add the `title` and `isCompleted` attributes:

```javascript
import DS from 'ember-data';

export default DS.Model.extend({
  title: DS.attr('string'),
  isCompleted: DS.attr('boolean')
});
```

## Using Fixtures

To enable fixtures run the command:

```
ember generate adapter application
```

and inside the `app/adapters/application.js` file replace `RESTAdapter` with `FixtureAdapter`.

```javascript
import DS from 'ember-data';

export default DS.FixtureAdapter.extend();
```

Now go back to our model `app/models/todo.js` and add a fixture to it. Also, make sure to create the `Todo` variable. The file should now look like:

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

Inside of `app/routes/todos.js` and place the following code:

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
```handlebars
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
```handlebars
<!--- ... additional lines truncated for brevity ... -->
<h1>todos</h1>
{{input type="text" id="new-todo" placeholder="What needs to be done?"
          value=newTitle action="createTodo"}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

Now we need to create a new controller for our todos so that we can something to handle our actions:

```
ember generate controller todos --type=array
```

This will generate a new file for us in `app/controllers/todos.js`. Edit this file so that it now looks like:

```javascript
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
```

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

Now lets create another controller:

```
ember generate controller todo --type=object
```

Inside of the `app/controllers/todo.js` file place the following code:

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
  {{input class="edit" value=title
                        focus-out="acceptChanges"
                        insert-newline="acceptChanges"
                        autofocus="autofocus"}}
{{else}}
<!--- ... additional lines truncated for brevity ... -->
```
{% endraw %}

In `app/controllers/todo.js` add the `acceptChanges` action:

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
  }
},
// ... additional lines truncated for brevity ...
```

## Deleting a Model

In `app/templates/todos.hbs` update the delete button:

{% raw %}
```handlebars
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

Create a new template for our child route:

```
ember generate route todos/index
```

Inside of `app/templates/todos.hbs` move the entire contents of `<ul id="todo-list"` section (including the `<ul></ul>` tags) into this new file: `app/templates/todos/index.hbs`.

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


Add the following code to `app/routes/todos/index.js`:

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

Let's generate a our 'active' route:

```
ember generate route todos/active
```

In `app/router.js` update the router add the active route under the 'todos' resource and be sure to clean up the 'todos/active' route created by the generator:

```javascript
import Ember from 'ember';
import config from './config/environment';

var Router = Ember.Router.extend({
  location: config.locationType
});

Router.map(function() {
  this.resource('todos', { path: '/' }, function() {
    this.route('active');
  });
});

export default Router;
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

Let's generate a new route for showing the completed tasks with:

```
ember generate route todos/completed
```

In `app/router.js` update the router add the 'completed' route under the 'todos' resource and be sure to clean up the 'todos/completed' route created by the generator:

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

I couldn't figure out how to get this to work with Ember CLI, but I will be writing another post that talks about how to connect to a Rails backend for data persistance.
