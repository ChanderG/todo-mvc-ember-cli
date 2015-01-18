# Todo-cli

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

* [Step 03 - Adding the first route](https://github.com/govidat/todo-cli/commit/5720334d0be33c5501e71b5ed68e73b76466bd54)
 
* [Step 04 - Modeling data/ Fixtures](https://github.com/govidat/todo-cli/commit/f48afb0c5cae27f3a9d467d72dda3e4cc3473b5e)

* [Step 05 - New Instance](https://github.com/govidat/todo-cli/commit/36f4c3f451a557cadce51d3c1e2178c1a29ea681)


## Step 05 - New Instance 

* edit app/templates/todo.hbs
~~~html
    <header id="header">
        <h1>todos</h1>
        {{input
          type="text"
          id="new-todo"
          placeholder="What needs to be done?"
          value=newTitle
          action="createTodo"}}
      </header>
~~~

$ ember generate controller todos
* edit app/controllers/todos.js and it should read as 
Note : Change Ember.Controller to Ember.ArrayController 
~~~html

import Ember from 'ember';

export default Ember.ArrayController.extend({
  actions: {
    createTodo: function() {
      // Get the todo title set by the "New Todo" text field
      var title = this.get('newTitle');
      if (!title.trim()) { return; }

      // Create the new Todo model
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
~~~
This controller will now respond to user action by using its newTitle property as the title of a new todo whose isCompleted property is false. Then it will clear its newTitle property which will synchronize to the template and reset the textfield. Finally, it persists any unsaved changes on the todo.

You should now be able to add additional todos by entering a title in the <input> and hitting the <enter> key.

* Marking a model as complete or incomplete

* edit app/templates/todos.hbs and change the <input> to {input}
Note : Addition of itemController="todo" in first line
Also todo.title. This is required to correctly get the item properties.

~~~html
          {{#each todo in model itemController="todo"}}
            <li {{bind-attr class="isCompleted:completed"}}>
              {{input type="checkbox" checked=todo.isCompleted class="toggle"}}
              <label>{{todo.title}}</label><button class="destroy"></button>
            </li>
          {{/each}} 
~~~

$ ember generate controller todo
* edit app/controllers/todos.js and it should read as 
Note : Change Ember.Controller to Ember.ObjectController 

~~~html
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

~~~
* Displaying the number of Incomplete Todos
* edit app/templates/todo.hbs
~~~html
	<span id="todo-count">
          <strong>{{remaining}}</strong> {{inflection}} left
    </span>
~~~
* edit app/controllers/todos.js and it should read as
Note: Add a , at the end of actions: {}
~~~html
  remaining: function() {
    return this.filterBy('isCompleted', false).get('length');
  }.property('@each.isCompleted'),

  inflection: function() {
    var remaining = this.get('remaining');
    return remaining === 1 ? 'item' : 'items';
  }.property('remaining')
~~~

* Toggling between showing and editing status
* edit app/templates/todo.hbs
~~~html
		<ul id="todo-list">
          {{#each todo in model itemController="todo"}}
            <li {{bind-attr class="todo.isCompleted:completed todo.isEditing:editing"}}>
              {{#if todo.isEditing}}
                <input class="edit">
              {{else}}
                {{input type="checkbox" checked=todo.isCompleted class="toggle"}}
                <label {{action "editTodo" on="doubleClick"}}>{{todo.title}}</label><button class="destroy"></button>
              {{/if}}  
            </li>
          {{/each}} 
        </ul>
~~~

* Inside app/controllers/todo.js add the the matching logic: 
Note : Pls note the , separator from previous content

~~~html
	....
  }.property('model.isCompleted'),

  actions: {
    editTodo: function() {
      this.set('isEditing', true);
    }
  },

  isEditing: false

~~~
$ ember generate adapter/view/helper edit-todo did not work properly
* Insert a file app/components/edit-todo.js

* edit app/components/edit-todo.js
* Refer : https://github.com/WMeldon/ember-cli-todos/blob/master/app/components/edit-todo.js
~~~html
import Ember from 'ember';

export default Ember.TextField.extend({
  didInsertElement: function() {
    this.$().focus();
    this.$().addClass('focus'); // headless testing is brittle
  }

});
~~~
* edit app/templates/todo.hbs
~~~html
              {{#if todo.isEditing}}
                {{edit-todo class="edit" value=todo.title focus-out="acceptChanges" insert-newline="acceptChanges"}}
              {{else}}
~~~

* edit app/controllers/todo.js and add...
~~~html
	...
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

    removeTodo: function () {
      var todo = this.get('model');
      todo.deleteRecord();
      todo.save();
    }
  },
  ...
 

~~~


