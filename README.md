# Todo-cli

I am a new comer to Ember and have been keenly following the [todo mvc tutorial] (http://emberjs.com/guides/getting-started/) in emberjs.com. 
Also came across nice tutorials on using ember-cli. 
 
This is my attempt to redo the same tutorial using ember-cli. I have tried to capture most of the steps that I have taken. This may be helpful for a novice and experienced folks may please excuse me for the verbosity. 

This document has evolved over multiple steps as envisaged in the [todo mvc tutorial] (http://emberjs.com/guides/getting-started/). More detailed steps have been specified in the end of this page.

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

* [Step 03 - Adding the first route](https://github.com/govidat/todo-cli/commit/5720334d0be33c5501e71b5ed68e73b76466bd54)
 
* [Step 04 - Modeling data/ Fixtures](https://github.com/govidat/todo-cli/commit/f48afb0c5cae27f3a9d467d72dda3e4cc3473b5e)

* [Step 05 - New Instance](https://github.com/govidat/todo-cli/commit/36f4c3f451a557cadce51d3c1e2178c1a29ea681)

* [Step 06 - Deleting Model to end](https://github.com/govidat/todo-cli/commit/be29a45378d355687b40aaef236038fade8aa184)

## Prerequisites

You will need the following things properly installed on your computer.

* [Git](http://git-scm.com/)
* [Node.js](http://nodejs.org/) (with NPM)
* [Bower](http://bower.io/)
* [Ember CLI](http://www.ember-cli.com/)
* [PhantomJS](http://phantomjs.org/)

## Installation

* `git clone <repository-url>` this repository
* change into the new directory
* `npm install`
* `bower install`

## Running / Development

* `ember server`
* Visit your app at [http://localhost:4200](http://localhost:4200).

### Running Tests

* `ember test`
* `ember test --server`

## Further Reading / Useful Links

* [ember.js](http://emberjs.com/)
* [ember-cli](http://www.ember-cli.com/)
* Development Browser Extensions
  * [ember inspector for chrome](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi)
  * [ember inspector for firefox](https://addons.mozilla.org/en-US/firefox/addon/ember-inspector/)

## Step 01 - Initialize Repository

* For a more detailed step by step flow pls refer README Step 01.md

* Setting up the environment

	As per links above ensure node, phantomjs and bower are installed. My versions are:
	$ node -v				// v0.10.33
	$ phantomjs -v	// 1.9.8
	$ bower -v			// 1.3.12 

* ember-cli

* Steps to remove watchman error

	Please refer the following links for details. I have followed them and performed the steps mentioned below.
  	* [Part 1](http://discuss.emberjs.com/t/could-not-find-watchman-falling-back-to-nodewatcher-for-file-system-events/6873)
  	* [Part 2](https://facebook.github.io/watchman/docs/install.html)

* Create a new ember 'todo-cli' application

* Run the ember server

	In localhost:4200 you will be able to see the output as follows:

## Step 02 - Creating a static mockup

* For a more detailed step by step flow pls refer README Step 02.md

*  The entry point into the application or the equivalent of index.html is in  app/templates/application.hbs. The extension .hbs denotes that this ia handlebar template. 

* Edit app/templates/application.hbs

* Replace the content of app/styles/app.css with [stylesheet](http://emberjs.com.s3.amazonaws.com/getting-started/style.css).
* Create a new subdirectory public/assets and place the file [backgroud image](http://emberjs.com.s3.amazonaws.com/getting-started/bg.png)
* localhost:4200 would have got refreshed on its own and you should get the following screen:

* Else you may stop the server (Ctrl C) and restart with $ ember server.
   
* Introduce app/templates/index.hbs

	The header, footer or any other static elements would remain in the application template. Additionally, we should have at least one {{outlet}}: a placeholder that the router will fill in with the appropriate template, based on the current URL. 

	Put the contents in index.hbs


* Edit app/templates/application.hbs

* localhost:4200 would have got refreshed on its own and you should get the same earlier screen of Fig 6.

## Step 03 - Adding the first route

* For a more detailed step by step flow pls refer README Step 03.md

* In the Ember Guide example, Adding the First Route and Template, a resource has been added to the router which corresponds to / URL and the template name is todos.

* We will use the ember generate command

* ember generate resource todos 

* Manually edit app/router.js file and add our resource:

* localhost:4200 will now give only the footer.  

* Initially the template was called index (app/templates/index.hbs) and it was corresponding to the default route indexRoute. Now, the route is todosRoute and the corresponding template expected is todos (app/templates/todos.hbs).

* This todos.hbs has already been generated by our earlier generate command. But is does not have any content and just has {{outlet}}

* Rename original index.hbs to todos.hbs 
* Now localhost:4200 is back to normal

## Step 04 - Modeling Data/ Fixtures / Displaying complete state

* For a more detailed step by step flow pls refer README Step 04.md

* In this part we will do the Ember Guide example - Modeling Data, Using Fixtures and Displaying the Model Data

* ember generate model todo title:string isCompleted:boolean

This completes "Modeling Data" of emberjs

* Using Fixtures

	Instead of using : ember generate adapter application

	create app/adapter/application.js and introduce the following lines: 
	import DS from 'ember-data';
 
	export default DS.FixtureAdapter.extend(); 

* Edit app/models/todo.js 

* Displaying Model Data

	Already the route todos.js has been created in the background when we generated the resource todos.

	* edit app/routes/todos.js

	Update the app/templates/todos.hbs and replace the static content. 

* Displaying Model's Complete State
	edit app/templates/todo.hbs and introduce {{bind-attr class="todo.isCompleted:completed"}} for <li>. 

## Step 05 - New Instance 

* For a more detailed step by step flow pls refer README Step 05.md

* edit app/templates/todo.hbs

	$ ember generate controller todos
* edit app/controllers/todos.js 

	This controller will now respond to user action by using its newTitle property as the title of a new todo whose isCompleted property is false. Then it will clear its newTitle property which will synchronize to the template and reset the textfield. Finally, it persists any unsaved changes on the todo.

* Marking a model as complete or incomplete

	* edit app/templates/todos.hbs and change the <input> to {input}
	Note : Addition of itemController="todo" in first line and also todo.title. This is required to correctly get the item properties.

	$ ember generate controller todo

	* edit app/controllers/todos.js

	Note : Change Ember.Controller to Ember.ObjectController 

* Displaying the number of Incomplete Todos
	
	* edit app/templates/todo.hbs

	* edit app/controllers/todos.js 

* Toggling between showing and editing status

	* edit app/templates/todo.hbs

	* Inside app/controllers/todo.js add the the matching logic: 
	Note : Pls note the , separator from previous content

	$ ember generate adapter/view/helper edit-todo did not work properly

	* Insert a file app/components/edit-todo.js

	* edit app/components/edit-todo.js
	* Refer : https://github.com/WMeldon/ember-cli-todos/blob/master/app/components/edit-todo.js

	* edit app/templates/todo.hbs

	* edit app/controllers/todo.js and add...

## Step 06 - Deleting Model / Adding Child Routes ... upto last step

* For a more detailed step by step flow pls refer README Step 06.md

* Deleting Model

	edit app/templates/todo.hbs

	In index.html update the static <button> element to include an {{action}} Handlebars helper:

	This will call the removeTodo action defined already and will delete the todo locally and then persist this data change.

	* Adding Child Routes

	* Copy app/templates/todos.hbs to app/templates/todos/index.hbs

	* Edit app/templates/todos/index.hbs and retain only the required part:

	* Edit app/templates/todos.hbs and retain only the required part:

* Modify the router to accomodate child routes:

	* Edit app/router.js

	* Note: The code mentioned for model has already been generated automatically when we generated resource todos. It is in app/routes/todos.js.

	When the application loads at the url '/' Ember.js will enter the todos route and render the todos template as before. It will also transition into the todos.hbs and fill the {{outlet}} in the todos template with the todos/index template.

* Transitioning to show only incomplete todos

	* Edit app/todos.hbs

	* edit app/router.js and include the child route active.

	* To create the relevant route active, we will use the ember-cli generate command. We need in a new subdirectory app/routes/todos/...

	$ ember generate route todos/active

	* edit app/routes/todos/active.js 

	The model data for this route is the collection of todos whose isCompleted property is false. When a todo's isCompleted property changes this collection will automatically update to add or remove the todo appropriately.

* Transitioning to show only complete todos
  
	* Edit app/todos.hbs

	* edit app/router.js and include the child route active.

	* To create the relevant route 'completed', we will use the ember-cli generate command. We need in a new subdirectory app/routes/todos/...

	$ ember generate route todos/completed

	* edit app/routes/todos/completed.js

* Transitioning back to show all todos

	* Edit app/todos.hbs

* Displaying a Button to Remove All Completed Todos

	* Edit app/todos.hbs

	* edit app/controller/todos.js

* Indicating When All Todos Are Complete

	* Edit app/todos.hbs

	* edit app/controller/todos.js

* Toggling All Todos Between Complete and Incomplete

	* edit app/controller/todos.js

## Step 07 - Adding Local Storage Adapter

* edit app/adapters/application.js

* instead of Fixture Adpater, Local storage adapter is introduced
~~~html
import DS from 'ember-data';
 
export default DS.LSAdapter.extend({
	namespace: 'todos'
});
~~~
* please refer https://github.com/kurko/ember-localstorage-adapter

* npm install --save-dev ember-localstorage-adapter
	
  This installs node_modules/ember-localstorage-adapter

  Now ember server works properly.

	The above reference mentions about modifying Brocfile.js and instructs to add:    	
~~~html
...
app.import('bower_components/ember-localstorage-adapter/localstorage_adapter.js');
~~~
	However this gives error. Even replacing bower_compnents/ with node_modules/ doesnot remove the error. Hence I have not modified the Brocfile.js and it works!

## Thanks. 
I will try to update this with tests in my next attempt. 