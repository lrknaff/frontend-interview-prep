#Interview Prep
> Common questions and things to study. 

##JavaScript
####What are the 2 most important paradigms of JS? Why?
* OOP
* Functional Programming
  - the use of functions as arguments

####Describe the difference between var, let and const

####What is a callback?
* Also know as a **higher-order function**.
* A function that is passed to another function as a parameter.
  - passed as an argument function defenition, not as an executed function. Does not have ().
* Call back functions are closures.
* Often called or executed inside the function it was called.
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
      - When functions exucute, they use the same scope chain that was in effect when they were created
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


####People in development I look up to

####What are promises? Why use them? Give an example of how to use them.

####Your favorite part about es6? Some examples of when you don't want to use es6.


##HTML/CSS
####Height of box around floats so that it doesn't disapear
* overflow: auto;

####What is a media query

####positives and negative of using a CSS pre-processer?
#####postives:

#####negatives:

####Resources:
[10 Questions Every JS Developer Should Know](https://medium.com/javascript-scene/10-interview-questions-every-javascript-developer-should-know-6fa6bdf5ad95#.wnhwoz4cx)
[What is a closure](http://javascriptissexy.com/understand-javascript-closures-with-ease/)