# Functions

Functions are fundamental building blocks, a function is a block of Js code that is defined once but may be executed or invoked any numbers of times, functions can have parameters where we can pass arguments trough it, In JavaScript, functions are objects, and they can be manipulated by programs.

## Types of functions

1. **function declaration:**
   are functions that are declared with the keyword `function`, this function have a keyword that is going to be the variable that is going to store the block of code, function declarations are hoisted in the top os the script_

```js
  function addition(x, y){
      let sum = x + y;
      return sum;
  }
```

2. **function expression:**
   A function expression declare a variable and assign the function to it you can declare de function assigned with the keyword `function` you can add a name if you are going to use recursion another way is the arrow function `=>`, is a compact declaration that do not use the keyword `function()` and name .
   Function expressions are not hoisted and in order to invoke it you have to declare it first

```js
  const f = function fact(x) { 
      if (x <= 1) {
          return 1
      } else {
          return x*fact(x-1); 
      };

  const addition = function(x, y){
      let sum = x + y;
      return sum;
  }
  // Arrow function 
  const addition = (x,y) => {return x + y};
  // Without the return keyword 
  const addition = (x,y) => x + y;
  // using only 1 parameter 
  const accumulator = x => x += x;
  // without parameter 
  const constantValue = () => 56;
  // returning objects 
  const f = x => { return { value: x }; }; // Good: f() returns an object
  const g = x => ({ value: x }); // Good: g() returns an object
```  

## Invoking functions

1. As functions
2. As methods
3. As constructors
4. Indirectly through their call() and apply() methods
5. •Implicitly, via JavaScript language features that do not appear like normal function invocations

## Method Chaining

