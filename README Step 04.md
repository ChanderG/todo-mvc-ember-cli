# Todo-cli

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

* [Step 03 - Adding the first route](https://github.com/govidat/todo-cli/commit/5720334d0be33c5501e71b5ed68e73b76466bd54)
 
* [Step 04 - Modeling data/ Fixtures](https://github.com/govidat/todo-cli/commit/f48afb0c5cae27f3a9d467d72dda3e4cc3473b5e)

## Step 04 - Modeling Data/ Fixtures / Displaying complete state

* In this part we will do the Ember Guide example - Modeling Data, Using Fixtures and Displaying the Model Data

* ember generate model todo title:string isCompleted:boolean

This completes "Modeling Data" of emberjs

* Using Fixtures

Instead of using : ember generate adapter application

create app/adapter/application.js and introduce the following lines: 
	import DS from 'ember-data';
 
	export default DS.FixtureAdapter.extend(); 

Edit app/models/todo.js and change to the following:
~~~html
import DS from 'ember-data';

var Todo = DS.Model.extend({
	title: DS.attr('string'),
	isCompleted: DS.attr('boolean')
}); 

Todo.reopenClass({
	FIXTURES: [
	{
		id: 1,
		title: 'Learn Ember.js',
		isCompleted: true
	},
	{
		id: 2,
		title: '...',
		isCompleted: false
	},
	{
		id: 3,
		title: 'Profit!',
		isCompleted: false
	}
	]
}); 

export default Todo;
~~~

* Displaying Model Data
Already the route todos.js has been created in the background when we generated the resource todos.

edit app/routes/todos.js and introduce two lines:
now it should look like:
~~~html
import Ember from 'ember';

export default Ember.Route.extend({
	model: function() {
		return this.store.find('todo');
	} 
});
~~~
Update the app/templates/todos.hbs and replace the static content with the following codes. It should read as :
~~~html
       <ul id="todo-list">
          {{#each}}
            <li>
              <input type="checkbox" class="toggle">
              <label>{{title}}</label><button class="destroy"></button>
            </li>
          {{/each}} 
        </ul>
~~~
* Displaying Model's Complete State
edit app/templates/todo.hbs and introduce {{bind-attr class="todo.isCompleted:completed"}} for <li>. It should read as :
~~~html
<li {{bind-attr class="isCompleted:completed"}}>
~~~
* localhost:4200 displays as earlier


