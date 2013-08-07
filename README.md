#Angular JS#

###What is it?###
Angular.js is 'HTML enhanced for Web Apps'. Essentially it tries to solve the problems of dynamic content and templates in HTML allowing you to write large scale single page web applications (ala Gmail). It is authored by Google and you can get a good look at applications built on it here:
http://builtwith.angularjs.org/

Don't let that put you off though, When you think about some of the tasks we have to manage now you can begin to find 'single page applications' dotted about the place.

###Why?###
Trying to make a large single page application often includes thousands of lines of javascript just to keep the DOM up to date and reflecting the changes you have made. Add in creation of HTML on the fly and you have some very messy spaghetti code. Essentially you are aiming to create slick, easy to use, maintainable applications.

###Where does this fit with Propeller?###
**Frontend**

Angular can create some great single page front end websites, We could convert most of our two days builds (which mostly seem to be single page anyway) to utilise angular and a rest API to handle CP content.

**Development**

Angular could be used inside some of our larger applications, but also as a base for some of our internal applications

- PropShop product manage page
- CMS Dashboard
- Changes System
- Bug Tracker

###The 'Updated' Basics###
At the most basic level we break down the DOM into the following:

- Template
- Page **(Controller)**
- Bindings

Our controller provides us with a tidy place to put functions for that **partial** (Essentially the same as a Fuel view). the **partial** would look like this:

```
  <span>{{remaining()}} of {{todos.length}} remaining</span>
    <ul class="unstyled">
    	<li ng-repeat="todo in todos">
        	<input type="checkbox" ng-model="todo.done">
          	<span class="done-{{todo.done}}">{{todo.text}}</span>
       	</li>
    </ul>
    <form ng-submit="addTodo()">
    	<input type="text" ng-model="todoText"  size="30"
               placeholder="add new todo here">
        <input class="btn-primary" type="submit" value="add">
   	</form>
```
This is a partial of a Todo list application. `todos` is our main model, which is specific to the **Controller** or **Scope**. The Controller for this example is below:

```
	function TodoCtrl($scope) {
  		$scope.todos = [
    		{text:'learn angular', done:true},
    		{text:'build an angular app', done:false}
    	];
 
  		$scope.addTodo = function() {
    		$scope.todos.push({text:$scope.todoText, done:false});
    		$scope.todoText = '';
  		};
 
  		$scope.remaining = function() {
    		var count = 0;
    		angular.forEach($scope.todos, function(todo) {
      			count += todo.done ? 0 : 1;
    		});
    		return count;
  		};
	}

```

From this example you should hopefully be able to see how the basic logic of the angular controller and partial work and how we can cut down on a large amount of frontend DOM updating.












