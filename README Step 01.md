# Todo-cli


* [Step 01 - Initialize repository](https://github.com/govidat/todo-cli/commit/e2251ea75eb8a504add51d8039b9e0d5c11a22ea)

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
   
