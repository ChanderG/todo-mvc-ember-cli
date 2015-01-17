# Todo-cli

I am a new comer to Ember and have been keenly following the [todo mvc tutorial] (http://emberjs.com/guides/getting-started/) in emberjs.com. 
Also came across nice tutorials on using ember-cli. 
 
This is my attempt to redo the same tutorial using ember-cli. I have tried to capture most of the steps that I have taken. This may be helpful for a novice and experienced folks may please excuse me for the verbosity. 

This document has evolved over multiple steps as envisaged in the [todo mvc tutorial] (http://emberjs.com/guides/getting-started/). More detailed steps have been specified in the end of this page.

* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

 
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

* Setting up the environment

	As per links above ensure node, phantomjs and bower are installed. My versions are:
	$ node -v				// v0.10.33
	$ phantomjs -v	// 1.9.8
	$ bower -v			// 1.3.12 

	For installing phantomjs and other requirements, it is better to run command like:

	$ npm install -g phantomjs

	-g flag is used to make these commands globally available at the command line.

* ember-cli 
	When I ran the following command I got an error:

	$ npm install -g ember-cli

	Error : npm ERR! Please try running this command again as root/Administrator.

	I ran the following with partial success:

	$ sudo npm install -g ember-cli  

	I got an output like: 

	npm WARN package.json ember-router-generator@0.1.0 No description
	/usr/bin/ember -> /usr/lib/node_modules/ember-cli/bin/ember
	ember-cli@0.1.5 /usr/lib/node_modules/ember-cli
	├── js-string-escape@1.0.0
	├── abbrev@1.0.5
	├── exit@0.1.2
	.....
	
	$ ember -v  // gave the following output

	version: 0.1.5
	Could not find watchman, falling back to NodeWatcher for file system events
	node: 0.10.33
	npm: 2.1.8

* Steps to remove watchman error

	Please refer the following links for details. I have followed them and performed the steps mentioned below.
  * [Part 1](http://discuss.emberjs.com/t/could-not-find-watchman-falling-back-to-nodewatcher-for-file-system-events/6873)
  * [Part 2](https://facebook.github.io/watchman/docs/install.html)

	$ git clone https://github.com/facebook/watchman.git
	Cloning into 'watchman'...
	...

	Checking connectivity... done.

	$ cd watchman

	$ ./autogen.sh

	configure.ac:21: installing './compile'

	...

	$ ./configure

	$ make

	$ sudo make install

	make[1]: Entering directory ...

* $ ember -v

	version: 0.1.5
	node: 0.10.33
	npm: 2.1.8

* Create a new ember 'todo-cli' application

	$ ember new todo-cli

	this takes a few minutes...
	Fig 2:
	

* Setting up the git-hub repository

	$ cd todo-cli

	$ git init

	$ git add -A

	$ git status

	Fig 1

	$ git commit -m "Initialize repository"

	Fig 3

* Run the ember server

	$ ember server

	In localhost:4200 you will be able to see the output as follows:
	Fig 4

* Bower dependencies

	If you get any error due to bower dependencies, you may run the following command.

	$ bower install

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
~~~
* Replace the content of app/styles/app.css with [stylesheet](http://emberjs.com.s3.amazonaws.com/getting-started/style.css).
* Create a new subdirectory public/assets and place the file [backgroud image](http://emberjs.com.s3.amazonaws.com/getting-started/bg.png)
* localhost:4200 would have got refreshed on otw own and you should get the following screen:
Fig 6.
* Else you may stop the server (Ctrl C) and restart with $ ember server.
   
