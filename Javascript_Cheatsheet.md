> # Function Defination & Function Declaration
```js
return_type myFunction() { // declaration
  // the body of the function (definition)
}
```
> # Typs of function in Javascript
* # Function Expression
```js
function function_name () { }

function_name()
```
***Note:*** 
This function is invoked by function name.


* # Anonymous Functions
```js
var function_name = function () { }

function_name();
```
***Note:***
This function is assign to a variable.
It can be invoked by using the variable.
It can be used as parameter inside another function.

* # Immediately Invoke Function Expression(IIFE)
```js
(function () { })();
```
***Note:***
This function executes immediately after the declaration.
The trailing paranthesis **( )** are used to invoke the function.


* # Constructor Functions
```js
var name = new Function(parameteres, functionBody);
```

* # Hoisting
```js
function_name();

function_name() {}
```

* # Arrow Functions
```js
() => "Hello World!";
() => { };
() => { return xyz; };
```