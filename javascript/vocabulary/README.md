#JavaScript Vocabulary
A place to define and reinforce JavaScript vocabulary in my own words.
##Closure
###Definition
A **Closure** is an inner function in JavaScript that's returned when we call it's parent function. This function has access to the variables defined inside of the parent function. The inner function returned retains it's original scope. So a variable defined inside of a parent function stays alive after the parent function is executed because the inner function retains a reference to the scope of the parent function (so the local variable is not garbage collected).
###Advantage
Using Closures prevents the global window object from becoming crowded with global variables.

###Disadvantage
This could lead to a memory leak because the reference to the inner variables of the parent function is never garbage collected. This is only a problem in large JavaScript applications though.
###Practical Example
* jQuery callbacks
* JavaScript Object Oriented code with public and private functions (http://stackoverflow.com/questions/2728278/what-is-a-practical-use-for-a-closure-in-javascript)

###Learning Resources
* https://www.youtube.com/watch?v=R_ZvxMyFSCU (very good explanation)
* https://www.youtube.com/watch?v=ZqGFKcCcO-Y (great explanation)
* https://www.youtube.com/watch?v=yiEeiMN2Khs

##IIFE (Immediately Invoked Function Expressions)
An **IIFE** is a function that's invoked immediately upon being defined. Used as a way to prevent populating the global namespace.

###Advantage
Prevented unwanted globals from leaking into the global scope. Also you can do a lot of logic at one time since you never need to call the function again.

Also useful when we need to run a piece of code multiple times. E.g. If you make a request to some API that returns JSON but the results are paginated. You need to call the function multiple times in order to get all the results. In this case, you will need to name this IIFE so it can call itself in order to retrive all the results (aka **recursion**).

###Disadvantage

###Practical Example
* jQuery plugins

###Learning Resources
* https://www.youtube.com/watch?v=KRm-h6vcpxs

##Hoisting
**Hoisting** is the process of using a variable before it's defined in a scope. Since variable declarations are processed before code is executed, declaring a variable anywhere in the code is the same as declaring it at the top. E.g. If I try to use a variable in a function before I declare it (but then later on declare and initialize it in the function scope), JavaScript will treat the declaration as if the variable had been declared *before* I used it. A variable is "hoisted" to the top of the variable scope. This variable will be hoisted to the top *without* the value I assigned to it.

###Practicle Example

####Good Code
```js
var myvar = 'my value';
// create a IIFE
(function() {
	alert(myvar);
})();
```
Executing this code produces an alert box with "my value". This is what should happen since "myvar" inside of the function scope has access to the global "myvar" variable, it will use that variable when it executes the code inside of the IIFE.

####Hoisting Example (with variables)
```js
var myvar = 'my value';

// create a IIFE
(function() {
	alert(myvar);
	var myvar = 'local value';

	alert(myvar);
})();
```
When this code runs, two alert boxes will be displayed with the first reading "undefined" and the second reading "local value".

####Why?
Because JavaScript treats the code as if it were written as:
###Practicle Example
```js
var myvar = 'my value';

// create a IIFE
(function() {
	// declare the "myvar" variable at the top
	var myvar;
	alert(myvar);
	// initialize the "myvar" variable
	myvar = 'local value';

	alert(myvar);
})();
```
The variable declaration was pushed to the top of the function scope but without being initialized with a value "local variable".

###More On Hoisting
Function declarations are "hoisted" to the top of their function scope but not function expressions.

####Hoisting Example (with function declarations)
```js
// create a IIFE
(function() {
	myNewFunction();

	function myNewFunction() {
		alert('local value');
	}
})();
```
Running this code will show an alert box reading "local value". This is because the function declaration was "hoisted" to the top of the function scope.
####Hoisting Example (with function expressions)
```js
// create a IIFE
(function() {
	
	newFunction();

	var newFunction = function () {
		alert('local value');
	}
})();
```
Running this code will cause a JavaScript error to be thrown. This is because the function expression was not "hoisted" to the top of the function scope. The declaration is moved to the top of the function scope but not the implementation.

JavaScript treats this as:
```js
// create a IIFE
(function() {
	var newFunction;
	newFunction();
	newFunction = function () {
		alert('local value');
	}
})();
```

###Learning Resources
* https://www.youtube.com/watch?v=sw49K4pxHCU
* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var#var_hoisting

##Event Bubbling
**Event Bubbling** is a way to propogate events in the DOM and occurs when an event happens on an element (e.g. click, hover, focus, etc...). It's a way to determine the order an event is received on elements. The inner element executes its callback first and then the outer element executes its callback second.

Bubble Up:
Outer element (execute a function second) <- Inner Element (execute a function first).

###Learning Resources
* http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing

##Event Capturing

Tricke Down:
Outer element (execute a function first) -> Inner Element (execute a function down).

###Learning Resources
* http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing