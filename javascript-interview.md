Java Script 
https://riyajain.hashnode.dev/most-frequent-javascript-questions-and-answers

call(), apply() and bind() Methods in JavaScript.

"this" always refers to an object.
"this" refers to an object which calls the function it contains.
In the global context “this” refers to either window object or is undefined if the ‘strict mode’ is 

.call() - calls the same function with the specified arguments

.apply() - calls the same function with the arguments specified in an array

.bind() - creates a new function with the same function body, with a preset value of this (the first argument) and returns that function.

In all cases, the first argument is used as the value of this inside the function.
```
var rtOne = {
    firstname: 'Rajendra',
    lastname: 'Taradale'
};

var rtTwo = {
    firstname: 'Sachin',
    lastname: 'Patil'
};

// this is common function - function borrowing / Your can create re-usable functions 
let printFullname = function() { 
  console.log("First Name-"+ this.firstname +" + LastName"+ this.lastname )
}

printFullname.call(rtOne) // First Name-Rajendra + LastNameTaradale
printFullname.call(rtTwo)  // First Name-Sachin + LastNamePatil

let printFullnamewithAddress = function(address){ console.log("First Name-"+ this.firstname +" + LastName "+ this.lastname +"  Address " + address ) }

printFullnamewithAddress.call(rtOne,"Pune")  // First Name-Rajendra + LastName Taradale  Address Pune
printFullnamewithAddress.apply(rtOne,["Mumbai"])  // First Name-Rajendra + LastName Taradale  Address Mumbai

Bind() - 

let newfun = printFullnamewithAddress.bind(rtOne,["Mumbai"]) 
newfun() // First Name-Rajendra + LastName Taradale  Address Mumbai

//Custom Bind Method - Polyfill 

Function.prototype.myRTbind = function(...args){
  let obj = this,
    params = args.slice(1);
  return function (...args2) {
    obj.apply(args[0], [...params, ...args2]);
  }
}

let newfunComplex = printFullnamewithAddress.mybind(rtOne, ["Mumbai"]);
newfunComplex("India");

```
