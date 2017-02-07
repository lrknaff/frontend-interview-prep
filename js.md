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
     - Objects and behaviors are typically tied together on the same entity, which mayb be accessed randomly by any number of functions. ==> *race conditions* and competition for resources
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
     - Can be confusing, becuase most people are used to OO programming
     - Steeper learning curve

####What is the difference between Protypal and Class inheritance?
* **Class inheritance**
  - instances inherit from classes (like a blueprint), and create sub-class relationshipes: heirarchical class taxonomies.
  - Instances typically instantiated via constructor functions with *'new'* keyword.
  - Creates tight coupling/hierarchies
  - NEVER appropriate, always favor composition over class inheritance
* **Prototypal inheritance**
  - Instances inherit directly from other objects.
  - Typically instantiated via factory functions with *'Object.create()'*
  - May be composed from many different objects, allowing for easy selective inheritance
  - Much easier to work with than class inheritance
  - *There are 3 types:*
     - **Delegation** (prototype chain)
     - **Concatenative** (mixins, 'Object.assign()')
     - **Functional** (A function used to create a closure for private state/encapsulation)
  - *When should you use this?*
     - When you need to compose objects from multiple sources
     - When you need inheritance

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
  - Implement better abstration where you can have more generic functions that are versatile (can handle all sorts of functionalities)

####What is event Bubbling/Delegation? Can you give an example?

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
* [Read](https://gist.github.com/domenic/3889970)

####Your favorite part about es6?
* [Read](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20&%20beyond/README.md#you-dont-know-js-es6--beyond)

####hat is Apply, Call and Bind methods? Why are they an essential part of JS?
* [Read](http://javascriptissexy.com/javascript-apply-call-and-bind-methods-are-essential-for-javascript-professionals/)

####What is two-way data binding and one-way data flow? How are they different?
* **Two-way data binding**: UI fields are bound to model data dynamically such that when a UI field changes, the model data changes with it
* **One-way data flow**: the model is the single source of truth. Changes in the UI trigger messages that signal user intent to the model (or “store” in **React**). Only the model has the access to change the app’s state. The effect is that data always flows in a single direction, which makes it easier to understand.

####What is asynchronous programming? Why is it important?
* Asynchronous programming means that the engine runs in an event loop. When a blocking operation is needed, the request is started, and the code keeps running without blocking for the result.
  - When the response is ready, an interrupt is fired, which causes an event handler to be run, where the control flow continues. In this way, a single program thread can handle many concurrent operations.
* This is important in JavaScript, because it is a very natural fit for user interface code, and very beneficial to performance on the server.
* Synchronous programming means that, barring conditionals and function calls, code is executed sequentially from top-to-bottom, blocking on long-running tasks such as network requests and disk I/O.