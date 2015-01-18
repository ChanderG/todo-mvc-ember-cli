# Todo-cli

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

* [Step 02 - Update mockup](https://github.com/govidat/todo-cli/commit/b407ff9a6ea1b9c5d65533add8c357fbf62d79bd)

## Step 02 - Creating a static mockup

*  The entry point into the application or the equivalent of index.html is in  app/templates/application.hbs. The extension .hbs denotes that this ia handlebar template. This template contains everything in between <body> tags, of a static html page.

*	Edit app/templates/application.hbs
	Replace the file contents with the following content:
		~~~html
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
		~~~
		* Replace the content of app/styles/app.css with [stylesheet](http://emberjs.com.s3.amazonaws.com/getting-started/style.css).
		* Create a new subdirectory public/assets and place the file [backgroud image](http://emberjs.com.s3.amazonaws.com/getting-started/bg.png)
		* localhost:4200 would have got refreshed on its own and you should get the following screen:
Fig 6.
		* Else you may stop the server (Ctrl C) and restart with $ ember server.
   
* Introduce app/templates/index.hbs

The header, footer or any other static elements would remain in the application template. Additionally, we should have at least one {{outlet}}: a placeholder that the router will fill in with the appropriate template, based on the current URL. 

Put the following contents in index.hbs
~~~html
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
		~~~	
	* Edit app/templates/application.hbs
		~~~html
		{{outlet}}

		<footer id="info">
			<p>Double-click to edit a todo</p>
		</footer> 
		~~~
	* localhost:4200 would have got refreshed on its own and you should get the same earlier screen of Fig 6.

