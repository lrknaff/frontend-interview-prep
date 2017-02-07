##JavaScript
####What are the 2 most important paradigms of JS? Why?
* OOP
* Functional Programming
  - the use of functions as arguments

####Describe the difference between var, let and const

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

####Your favorite part about es6?