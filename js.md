##JavaScript
####What are the 2 most important paradigms of JS? Why?
* **OOP (Object Oriented Programming)**
  - Supports prototypal inheritance
  - Objects without classes
  - **Pros:**
     - Easy to interpret and read
     - Tend to be imperative rather than declarative, which reads like a straight-forward set of instructions.
  - **Cons:**
     - Typically depends on shared state
     - Objects and behaviors are typically tied together on the same entity, which may be accessed randomly by any number of functions. ==> *race conditions* and competition for resources
* **Functional Programming**
  - Supported by the use of functions as arguments, closures, higher order functions, lambdas
  - Produces programs by composing mathematical functions
  - Avoids shared state & mutable data
  - Uses pure functions
  - **Pros:**
     - Avoid shared state or side-effects
     - More simplified and easier to recompose and reuse
     - Tends to favor declarative styles
     - Can refactor with very little code change
     - Removes fear of resource conflicts and *race conditions*
  - **Cons:**
     - Over exploitation can reduce readability through abstraction
     - Can be confusing, because most people are used to OO programming
     - Steeper learning curve

####What is the difference between Prototypal and Class inheritance?

* **Class inheritance**
  - instances inherit from classes (like a blueprint), and create sub-class relationships: heirarchical class taxonomies.
  - Instances typically instantiated via constructor functions with *'new'* keyword.
  - Creates tight coupling/hierarchies
  - NEVER appropriate, always favor composition over class inheritance
* **Prototypal inheritance**
  - Instances inherit directly from other objects.
  - Typically instantiated via factory functions with *'Object.create()'*
  - May be composed from many different objects, allowing for easy selective inheritance
  - Much easier to work with than class inheritance
  - *There are 3 types:*
     - [Read](https://medium.com/javascript-scene/3-different-kinds-of-prototypal-inheritance-es6-edition-32d777fa16c9#.vs44bdiyf)
     - **Delegation** (prototype chain)
     - **Concatenative** (mixins, 'Object.assign()')
     - **Functional** (A function used to create a closure for private state/encapsulation)
  - *When should you use this?*
     - When you need to compose objects from multiple sources
     - When you need inheritance

####How many data types are there in JS/What are they?
Different interviewers will likely have different opinions on this, but the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures) define six main JS data types:
* String
* Number (note that JS does not distinguish in type assignment between integers and decimals)
* Boolean
* Undefined (when a variable is referenced that does not have a value)
* Null (an assigned value; the intentional assignment of a var to a value of nothing)
* Object (includes Function, Array, and Object)

####Why are Functions and Arrays considered Objects in JS?
JS was written to be an object oriented language. All objects in JS, broadly defined, inherit from `Object.prototype`, while arrays inherit from `Array.prototype` and functions from `Function.prototype`, which in turn inherit from `Object.Prototype.` This structure has shaped the language and its emphasis on prototypal inheritance as a core data architecture. 

####Be able to implement a simple application using ES6 classes and prototypal inheritance.
This is a technical interview question that can cause problems for unprepared applicants. For more details, see [this repo](https://github.com/gness1804/comment-section)

####Describe the difference between var, let and const
* **const**:
  - es6, identifier **cannot** be reassigned
  - Use when you do not need to reassign a variable. (most of the time)
  - block scoped
  - Not immutable. You can update the properties
* **let**:
  - Use when you need to reassign a variable.
  - Examples: for loops or mathematical algorithms
  - block scoped
* **var**:
  - There is not really a use case to use this in ES6.
  - function scoped
* WARNING: 'let' and 'const' variables cannot be checked using 'typeof' because of lexical scope

####What is a callback?
* [Description](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/)
* Also know as a **higher-order function**.
* A function that is passed to another function as a parameter.
  - passed as an argument function definition, not as an executed function. Does not have ().
* Call back functions are closures.
* Often called or executed inside the function it was called.
* Often used in these ways:
  - Asynchronous execution
  - Event Listeners/Handlers
  - setTimeout/setInterval methods
  - Generalization: code conciseness
* Derived from **functional programming**
* You can use named OR anonymous functions.
  - examples using anonymous functions:

   ```
   //Note that the item in the click method's parameter is a function, 	not a variable.​
	​//The item is a callback function
	$("#btn_1").click(function() {
	  alert("Btn 1 Clicked");
	});

	//javascript example
	var friends = ["Mike", "Stacy", "Andy", "Rick"];
​
	friends.forEach(function (eachName, index){
	console.log(index + 1 + ". " + eachName); // 1. Mike, 2. Stacy, 3. 	Andy, 4. Rick​
	});
	```

  - example using named function:

  ```
   // global variable​
​var allUserData = [];
​
​// generic logStuff function that prints to console​
​function logStuff (userData) {
    if ( typeof userData === "string")
    {
        console.log(userData);
    }
    else if ( typeof userData === "object")
    {
        for (var item in userData) {
            console.log(item + ": " + userData[item]);
        }
​
    }
​
}
​
​// A function that takes two parameters, the last one a callback function​
​function getInput (options, callback) {
    allUserData.push (options);
    callback (options);
​
}
​
​// When we call the getInput function, we pass logStuff as a parameter.​
​// So logStuff will be the function that will called back (or executed) inside the getInput function​
getInput ({name:"Rich", speciality:"JavaScript"}, logStuff);
​//  name: Rich​
​// speciality: JavaScript
  ```
* It is a good idea to check if the callback function is indeed a function
  ``if (typeof callback === "function") {
        callback(options);}``

* Avoid **callback hell**
* Benefits of callbacks
  - DRY, more readable
  - Maintainable
  - Implement better abstraction where you can have more generic functions that are versatile (can handle all sorts of functionalities)

####What is event Bubbling/Delegation? Can you give an example?
* [Read](https://learn.jquery.com/events/event-delegation/)
* **Event Bubbling/Propagation:** An event received by an element doesn't stop with that one element. It moves to other elements like the parent, and other ancestors of the element.
* **Event Delegation:** Event delegation allows us to attach a single event listener, to a parent element, that will fire for all descendants matching a selector, whether those descendants exist now or are added in the future.
  - Uses event propagation (bubbling) to handle events at a higher level in the DOM than the element on which the event originated.
  - Example of using **event delegation** (The second, selector parameter tells the handler to listen for the specified event, and when it hears it, checks to see if the triggering element for that event matches the second parameter):

  ```
  // Attach a delegated event handler
	$( "#list" ).on( "click", "a", function( event ) {
    event.preventDefault();
    console.log( $( this ).text() );
});
  ```

####What is a closure?
* [explanation](http://javascriptissexy.com/understand-javascript-closures-with-ease/)
* [more about closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
*  closure is the combination of a function and the lexical environment (or simply "environment") within which that function was declared.
* An inner function that has access to the outer (enclosing) function's variables -- scope chain. The closure has 3 scope chains
	- Access to it's own scope
	- Access to outer function's variables
	- Access to the global variables
- The inner function has access to both the outer function's variables and parameters.
  	- **Inner function, however, cannot call the outer function's arguments object.**
- 	Why use it?
   	- to store a private variable within an outer function
   	- Can write in a single method instead of an Object
- To create a closure you add a function inside of another function:

```
function showName (firstName, lastName) { 
​var nameIntro = "Your name is ";
    // this inner function has access to the outer function's variables, including the parameter​
​function makeFullName () {         
​return nameIntro + firstName + " " + lastName;     
}
​
​return makeFullName (); 
} 
​
showName ("Michael", "Jackson"); // Your name is Michael Jackson
```

- jQuery example:

```
$(function() {
​
​var selections = [];
$(".niners").click(function() { // this closure has access to the selections variable​
selections.push (this.prop("name")); // update the selections variable in the outer function's scope​
});
​
});
```

- Rules and Side Effects
   - The inner function **still** has access to the outer function's variables even after the function returns
      - When functions execute, they use the same scope chain that was in effect when they were created
  - Closures store references to the outer function's variables
      - They do not store the actual value. If the outer function's variable changes the closure will note and use that change
  - If the outer function's variable changes it can lead to bugs. (i.e. with a for loop)

  	```
	// This example is explained in detail below (just after this code box).​
​function celebrityIDCreator (theCelebrities) {
    var i;
    var uniqueID = 100;
    for (i = 0; i < theCelebrities.length; i++) {
      theCelebrities[i]["id"] = function ()  {
        return uniqueID + i;
      }
    }

    return theCelebrities;
}
​
​var actionCelebs = [{name:"Stallone", id:0}, {name:"Cruise", id:0}, {name:"Willis", id:0}];
​
​var createIdForActionCelebs = celebrityIDCreator (actionCelebs);
​
​var stalloneID = createIdForActionCelebs [0];  console.log(stalloneID.id()); // 103 
  	```
      - To fix this you can **immediately invoke a function expression**
      - or use let, instead of var since the closure will bind the block scoped variable.

    ```
      function celebrityIDCreator (theCelebrities) {
    var i;
    var uniqueID = 100;
    for (i = 0; i < theCelebrities.length; i++) {
        theCelebrities[i]["id"] = function (j)  { // the j parametric variable is the i passed in on invocation of this IIFE​
            return function () {
                return uniqueID + j; // each iteration of the for loop passes the current value of i into this IIFE and it saves the correct value to the array​
            } () // BY adding () at the end of this function, we are executing it immediately and returning just the value of uniqueID + j, instead of returning a function.​
        } (i); // immediately invoke the function passing the i variable as a parameter​
    }
​
    return theCelebrities;
}
​
​var actionCelebs = [{name:"Stallone", id:0}, {name:"Cruise", id:0}, {name:"Willis", id:0}];
​
​var createIdForActionCelebs = celebrityIDCreator (actionCelebs);
​
​var stalloneID = createIdForActionCelebs [0];
 console.log(stalloneID.id); // 100​
​
​var cruiseID = createIdForActionCelebs [1]; console.log(cruiseID.id); // 101

      ```


####What are promises? Why use them? Give an example of how to use them.
* [You're Missing the Point of Promises.](https://gist.github.com/domenic/3889970)
* [What's the Point of Promises?](http://www.telerik.com/blogs/what-is-the-point-of-promises)
* A promise represents the eventual result of an asynchronous operation. It is a placeholder into which the successful result value or reason for failure will materialize.
* A promise is an object that requires one method: **then**
  - **then** takes up to three arguments (success callback, failure callback, and progress callback)
* A promise can be in one of three states:
  - unfulfilled
  - fulfilled
  - failed
* Why use promises?
  - to avoid *callback hell* or the *pyramid of doom*
  - Makes things much easier to read
  - Parallel synchronous operations

####How does one pinpoint the source of an error in a lengthy promise chain? 
One can use `.catch()` or a second callback to `.then()` to trigger when a given promise fails.

####Your favorite part about es6?
* [Read](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20&%20beyond/README.md#you-dont-know-js-es6--beyond)
* Subjective opinion.
* Some ideas:
  - template literals
  - default parameters
  - destructuring
  - arrow functions
  - promises
  - let and const

####What are Apply, Call and Bind methods? Why are they an essential part of JS?
* [JavaScript’s Apply, Call, and Bind Methods are Essential for JavaScript Professionals](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/)
* **Bind:** The *Bind()* method is used primarily to call a function with the *this* value set explicitly.
  - the need for this usually occurs when you use the *this* keyword in a method from a receiver object; in such cases, sometimes *this* is not bound to the object you would expect it to be bound to.
  - Example:

  ```
  //            <button>Get Random Person</button>​
​//        <input type="text">​
​
​
​var user = {
    data        :[
        {name:"T. Woods", age:37},
        {name:"P. Mickelson", age:43}
    ],
    clickHandler:function (event) {
        var randomNum = ((Math.random () * 2 | 0) + 1) - 1; // random 	number between 0 and 1​
​
        // This line is adding a random person from the data array to 	the text field​
        $ ("input").val (this.data[randomNum].name + " " + 	this.data[randomNum].age);
    	}
​
	}
  $ ("button").click (user.clickHandler.bind (user));
  ```

  - Can also use for *currying*: passing one or more arguments. The function then has access to stored arguments and variables of the outer function.
* **Apply/Call:** Allow us to borrow functions and set the *this* value in function invocation.
  - *Apply* function in particular allows us to execute a function with an array of parameters, such that each parameter is passed to the function individually when the function executes.
     - great for **variadic** functions; which takes a varying number of arguments, not a set number like most functions.
  - Can be used to set the *this* value
  - The most common use is for **borrowing functions**
     - borrowing array methods from array-like objects

     ```
     // An array-like object: note the non-negative integers used as keys​
                var anArrayLikeObj = {0:"Martin", 1:78, 2:67, 3:["Letta", "Marieta", "Pauline"], length:4 };
     ```
     Now, if wish to use any of the common Array methods on our object, we can:

     ```
     // Make a quick copy and save the results in a real array:​
                // First parameter sets the "this" value​
                var newArray = Array.prototype.slice.call (anArrayLikeObj, 0);
​
                console.log (newArray); // ["Martin", 78, 67, Array[3]]​
​
                // Search for "Martin" in the array-like object​
                console.log (Array.prototype.indexOf.call (anArrayLikeObj, "Martin") === -1 ? false : true); // true​
​
                // Try using an Array method without the call () or apply ()​
                console.log (anArrayLikeObj.indexOf ("Martin") === -1 ? false : true); // Error: Object has no method 'indexOf'​
​
                // Reverse the object:​
                console.log (Array.prototype.reverse.call (anArrayLikeObj));
                // {0: Array[3], 1: 67, 2: 78, 3: "Martin", length: 4}​
​
                // Sweet. We can pop too:​
                console.log (Array.prototype.pop.call (anArrayLikeObj));
                console.log (anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, length: 3}​
​
                // What about push?​
                console.log (Array.prototype.push.call (anArrayLikeObj, "Jackie"));
                console.log (anArrayLikeObj); // {0: Array[3], 1: 67, 2: 78, 3: "Jackie", length: 4}​
     ```
     - Borrow 'string' methods
     - Borrow other methods and functions

####What is two-way data binding and one-way data flow? How are they different?
* **Two-way data binding**: UI fields are bound to model data dynamically such that when a UI field changes, the model data changes with it
* **One-way data flow**: the model is the single source of truth. Changes in the UI trigger messages that signal user intent to the model (or “store” in **React**). Only the model has the access to change the app’s state. The effect is that data always flows in a single direction, which makes it easier to understand.

####What is asynchronous programming? Why is it important?
* Asynchronous programming means that the engine runs in an event loop. When a blocking operation is needed, the request is started, and the code keeps running without blocking for the result.
  - When the response is ready, an interrupt is fired, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations.
* This is important in JavaScript, because it is a very natural fit for user interface code, and very beneficial to performance on the server.
* Synchronous programming means that, barring conditionals and function calls, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.

####What is console shimming?
* A workaround when a browser has no or incomplete console support. Since the console is so critical for JS debugging, it's necessary to have access to one in a browser. Console shimming typically involves creating a dummy console and/or fallback functions for cases when browsers' native consoles are insufficient. For more info, see [this repo](https://github.com/kayahr/console-shim)

####Describe the difference between a cookie, sessionStorage and localStorage.
* [Client Side Storage](https://github.com/turingschool/lesson_plans/blob/3ee469be5fdc94c926a88ca510106848b0339731/ruby_04-apis_and_scalability/client_side_storage.markdown)
* **Cookies**:
	- Before HTML5 was introduced, the primary mechanism for storing information in the browser was cookies.
	- Limitations:
		- Not able to hold a lot of data (a limit of 4095 bytes)
		- Sent to the server every time you request a page from that domain
		- Not considered secure. Cookies are vulnerable to cross-site request forgery (CSRF) 	
* **Local Storage and Session Storage**: ML5 introduced a storage object to help users store data in the browser. The storage object has two different types localStorage and sessionStorage and both types share the same methods.
* They both store data in Key/Value pairs of strings.
* To protect the user, the data stored in localStorage and sessionStorage is shared only under the same origin policy - meaning that it is stored in the browser but only accessible to pages with the same domain as that which stored it.
	- **Session Storage**: does not persist outside of the users session - useful for semi-private user information or rapidly changing data.
	- **Local Storage**: persists across tabs and is useful for data that should be stored offline.

####Difference between: function Person(){}, var person = Person(), and var person = new Person()?
* [Different Ways of Defining Functions](http://davidbcalhoun.com/2011/different-ways-of-defining-functions-in-javascript-this-is-madness/)
* `function Person(){`: function declaration. Needs a name.
* `var person = Person()`: function expression. Can be anonymous `var B = function(){};`. Do to hoisting, order matters.
* `var person = new Person()`: function constructor

####What is the difference between == and ===
* [Equality Comparisons](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)
* `==`: Abstract Equality Comparison. Loose or 'Abstract' equality compares two value for equality, *after* converting both values to a common type
* `===`: Strict Equality Comparison. Compare two values for equality

####Question: What is the value of foo?
* `var foo = 10 + '20';`=== '1020'

####Question: What value is returned from the following statement?
`"i'm a lasagna hog".split("").reverse().join("");` === "goh angasal a m'i"

####Explain event delegation
* [Event Bubbline and Delegation](http://frontend.turing.io/lessons/event-bubbling-and-delegation.html)

####What does CORS stand for and what issue does it address?
* [CORS](http://frontend.turing.io/lessons/cors.html)

####Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
* [Read](http://frontend.turing.io/lessons/module-1/js-2.html)

####Explain why the following doesn't work as an IIFE: function foo(){ }();
* [Scopes and Closures](https://docs.google.com/presentation/d/1zX-A4d_yMFPrVpofoIP5FLSjOb94vBzORql-BOV2vUc/edit#slide=id.g1c494e40cb_0_48)
* [IIFE](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)
* What needs to be changed to properly make it an IIFE?

####How do you serve a page with content in multiple languages?
* [Localization](http://frontend.turing.io/lessons/localization.html)

####What is "use strict";? what are the advantages and disadvantages to using it?
* [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)

####What are the pros and cons of using Promises instead of callbacks?
* [Making and Keeping Promises](http://frontend.turing.io/lessons/promises.html)
* [ES6 Generators](http://frontend.turing.io/lessons/es6-generators.html)

####Explain Ajax in as much detail as possible.
* [Ajax Intro](https://www.w3schools.com/xml/ajax_intro.asp)
* [jQuery Ajax](http://api.jquery.com/jquery.ajax/)

####What is a function declaration versus function expression? 
* A function declaration is simply instantiating a function, like so: 
```
  function foo () {
    console.log('foobar')
    }
```

A function expression, by contrast, is a function that is either set equal to a variable (expresses a relationship) or an IIFE (Immediately Invoked Function Expression): 
```
  var foo = function(){
    console.log('foobar')}  
```
The two examples above are very similar, except that the latter is not hoisted, as explained in the next section. Another difference between function expressions and function declarations is that function declarations must be named, while function expressions can be anonymous. (See the section in IIFEs below for more discussion on them).

####What is hoisting, and why does it matter? 
* Hoisting is JavaScript's behavior of putting declarations into memory before actually executing code. What this means is that one can write a var declaration below a function using that variable, and the code will still run because the var declaration is put into memory before the function is executed. Similarly, functions can be declared below where they are called, and hoisting works the same way (function expressions, however, are not hoisted, meaning that they must be instantiated before they are referenced). An example from the [MDN docs](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting): 

```

catName("Chloe");

function catName(name) {
    console.log("My cat's name is " + name);
}
/*
The result of the code above is: "My cat's name is Chloe"
*/
```
Note, however, that JS only hoists declarations (like var x;) NOT expressions (var x = 2). This means that you must initialize a var (set it to an actual value) before referencing it, or it will return undefined. The code below, from the same MDN doc, will throw an error for this reason:

```
  var x = 1; // Initialize x
  console.log(x + " " + y);  //y is undefined
  var y = 2;
  //the above code and the below code are the same

  var x = 1; // Initialize x
  var y; // Declare y
  console.log(x + " " + y);  //y is undefined
  y = 2; // Initialize y
```

####What are Immediately Invoked Function Expressions (IIFEs)?
IIFEs are functions that are called immediately once they are created. By contrast, a regular function must be called separately, via a function call like `getData()`. An IIFE looks like this:
```
  (function getData(){
    console.log('I will get the data as soon as the JS engine reads me!')
    })():
```
IIFEs are often used to protect data from the global scope. They can also be useful if one wants to execute code when the page loads and doesn't want to bother with something like a `load` event listener or adding an additonal line of code to call a previously created function. 

####What is meant by the term "code coverage" in JS? 
This term refers to test coverage; that is, how much of your code is covered by tests. The more thorough your tests test the app, the better your code coverage is.
