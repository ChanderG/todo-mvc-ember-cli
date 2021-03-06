# Todo-cli


* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

* [Step 03 - Adding the first route](https://github.com/govidat/todo-cli/commit/5720334d0be33c5501e71b5ed68e73b76466bd54)

 

## Step 03 - Adding the first route

* In the Ember Guide example, Adding the First Route and Template, a resource has been added to the router which corresponds to / URL and the template name is todos.

* We will use the ember generate command

* ember generate resource todos 

	Fig 7

* Manually edit app/routes.js file and add our resource:
~~~html

	import Ember from "ember";
	import config from "./config/environment";

	var Router = Ember.Router.extend({
	  location: config.locationType
	});

	Router.map(function() {
	  this.resource("todos", { path: '/' });
	});

	export default Router;
~~~

* localhost:4200 will now give only the footer.  
* Initially the template was called index (app/templates/index.hbs) and it was corresponding to the default route indexRoute. Now, the route is todosRoute and the corresponding template expected is todos (app/templates/todos.hbs).
* This todos.hbs has already been generated by our earlier generate command. But is does not have any content and just has {{outlet}}

* Rename original index.hbs to todos.hbs 
* Now localhost:4200 is back to normal
