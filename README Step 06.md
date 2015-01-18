# Todo-cli

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

* [Step 03 - Adding the first route](https://github.com/govidat/todo-cli/commit/5720334d0be33c5501e71b5ed68e73b76466bd54)
 
* [Step 04 - Modeling data/ Fixtures](https://github.com/govidat/todo-cli/commit/f48afb0c5cae27f3a9d467d72dda3e4cc3473b5e)

* [Step 05 - New Instance](https://github.com/govidat/todo-cli/commit/36f4c3f451a557cadce51d3c1e2178c1a29ea681)

* [Step 06 - Deleting Model to end](https://github.com/govidat/todo-cli/commit/be29a45378d355687b40aaef236038fade8aa184)


## Step 06 - Deleting Model / Adding Child Routes ... upto last step

* Deleting Model

edit app/templates/todo.hbs

In index.html update the static <button> element to include an {{action}} Handlebars helper:

~~~html
  <button {{action "removeTodo"}} class="destroy"></button>
~~~

This will call the removeTodo action defined already and will delete the todo locally and then persist this data change.

* Adding Child Routes

In app/templates/todo.hbs move the entire '<ul>'' of todos into a new template named app/templates/todos/index.hbs by adding a new Handlebars template "<script>" tag inside the "<body>" of the document:

* Copy app/templates/todos.hbs to app/templates/todos/index.hbs

* Edit app/templates/todos/index.hbs and retain only the following part:
~~~html
        <ul id="todo-list">
          {{#each todo in model itemController="todo"}}
           ...
           ...
           ... 
          {{/each}} 
        </ul>
~~~

* Edit app/templates/todos.hbs and retain only the following part:
~~~html
      ...
      ...
      <section id="main">
        {{outlet}}
        <input type="checkbox" id="toggle-all">
      </section>
      ...
      ...
~~~

* Modify the router to accomodate child routes:
* Edit app/router.js
~~~html
...
Router.map(function() {
  this.resource("todos", { path: '/' }, function () {
    // additional child routes will go here later
  });
});
...
~~~

* Note: The code mentmlioned for model has already been generated automatically when we generated resource todos. It is in app/routes/todos.js.

When the application loads at the url '/' Ember.js will enter the todos route and render the todos template as before. It will also transition into the todos.hbs and fill the {{outlet}} in the todos template with the todos/index template.

* Transitioning to show only incomplete todos
* Edit app/todos.hbs
~~~html
<li>
  <a href="all">All</a>
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  <a href="completed">Completed</a>
</li>
~~~

* edit app/router.js and include the child route active.
~~~html
.....
Router.map(function() {
  this.resource("todos", {
    path: "/"
  }, function() {
    this.route("active");

~~~

* To create the relevant route active, we will use the ember-cli generate command. We need in a new subdirectory app/routes/todos/...
$ ember generate route todos/active
* edit app/routes/todos/active.js and it should read as follows:
~~~html
import Ember from 'ember';

export default Ember.Route.extend({
  model: function(){
    return this.store.filter('todo', function(todo) {
      return !todo.get('isCompleted');
    });
  },
  renderTemplate: function(controller) {
    this.render('todos/index', {controller: controller});
  }
  
});

~~~

The model data for this route is the collection of todos whose isCompleted property is false. When a todo's isCompleted property changes this collection will automatically update to add or remove the todo appropriately.

* Transitioning to show only complete todos
  
* Edit app/todos.hbs
~~~html
<li>
  <a href="all">All</a>
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  {{#link-to "todos.completed" activeClass="selected"}}Completed{{/link-to}}
</li>
~~~
* edit app/router.js and include the child route active.
~~~html
.....
Router.map(function() {
  this.resource("todos", {
    path: "/"
  }, function() {
    this.route("active");
    this.route("completed");

~~~

* To create the relevant route 'completed', we will use the ember-cli generate command. We need in a new subdirectory app/routes/todos/...
$ ember generate route todos/completed
* edit app/routes/todos/completed.js and it should read as follows:
~~~html
import Ember from 'ember';

export default Ember.Route.extend({
  model: function(){
    return this.store.filter('todo', function(todo) {
      return todo.get('isCompleted');
    });
  },
  renderTemplate: function(controller) {
    this.render('todos/index', {controller: controller});
  }
  
});

~~~

* Transitioning back to show all todos
* Edit app/todos.hbs
~~~html
<li>
  {{#link-to "todos.index" activeClass="selected"}}All{{/link-to}}
</li>
<li>
  {{#link-to "todos.active" activeClass="selected"}}Active{{/link-to}}
</li>
<li>
  {{#link-to "todos.completed" activeClass="selected"}}Completed{{/link-to}}
</li>
~~~

* Displaying a Button to Remove All Completed Todos
* Edit app/todos.hbs
~~~html
{{#if hasCompleted}}
  <button id="clear-completed" {{action "clearCompleted"}}>
    Clear completed ({{completed}})
  </button>
{{/if}}
~~~

* edit app/controller/todos.js
~~~html
  ....
  actions: {
    createTodo: function() {
      ....
    },

    clearCompleted: function() {
      var completed = this.filterBy('isCompleted', true);
      completed.invoke('deleteRecord');
      completed.invoke('save');
    }  

  },

  remaining: function() {
    ...),

  hasCompleted: function() {
    return this.get('completed') > 0;
  }.property('completed'),

  completed: function() {
    return this.filterBy('isCompleted', true).get('length');
  }.property('@each.isCompleted')
  

~~~

* Indicating When All Todos Are Complete
* Edit app/todos.hbs
~~~html
...
      <section id="main">
        {{outlet}}
          {{input type="checkbox" id="toggle-all" checked=allAreDone}}
      </section>
~~~

* edit app/controller/todos.js
~~~html
  ....

  remaining: function() {
    ...),
  allAreDone: function(key, value) {
    return !!this.get('length') && this.isEvery('isCompleted');
  }.property('@each.isCompleted')

~~~

* Toggling All Todos Between Complete and Incomplete
* edit app/controller/todos.js
~~~html
...

allAreDone: function(key, value) {
  if (value === undefined) {
    return !!this.get('length') && this.isEvery('isCompleted', true);
  } else {
    this.setEach('isCompleted', value);
    this.invoke('save');
    return value;
  }
}.property('@each.isCompleted')
~~~

