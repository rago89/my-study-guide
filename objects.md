# Objects

Is an unordered list of properties this properties are composed of key-values, everything that is not a primitive type is an object, objects differ from primitive types because they are mutable, objects can have as properties functions which are going to be methods of that object.

The properties of objects cannot have repeated keys name, rule that is valid to the values

Functions are objects and they have their own methods this methods like call, apply and bind they can be use to pass the property of an object in to another or use the prototype to call methods

Objects are passed by reference it means that if you modify the object is going to be also modified it's reference, to avoid that you have to create an empty object and copy the values of it.

## Creating objects

1. **Objects literal**: is create an object manually `let obj = {}`
2. **new Object();** you can create a new empty object or create a new object with the inherited properties of another object
3. **Object.create();** create an object using the first argument as prototype of that object, it's like keeping a backpack without modifying the new properties created from that object, if the properties of the original object are modified the prototype of the new object will be modified, and if I try to change the value of one of the inherited properties, what I will be doing is creating a new own property

 ```js
  'use strict';
  let obj1 = { x: 1 };
  let obj2 = Object.create(obj1);
  obj2.y = 2;

  /*----  scope ----*/
  obj2:
  y: 2
  __proto__:
  x: 1
  __proto__: Object
  ```

4. **Spread operator** can copy an object without referring the object copied

  ```JS
  let obj1 = { x: 1 };
  let obj2 = {...obj1};
  console.log(obj2); //=> { x: 1 } 
  ```

## Querying object properties

- Can be querying by dot notation

```js
  let obj = { x: 1 }; // object literal 
  o.x // => 1;
```

- Can be query as bracket notation named also interpreted like object As associative arrays

```js
  let obj = { x: 1 }; // object literal 
  o['x'] // => 1;
```

## deleting properties

To delete a property is use the delete keyword, if you try to delete an property that doesn't exist is no going to be ani error and also nothing is going to happen, when you delete a property of an object where it was created it will delete also in the prototype chain

if you create a configurable property using globalThis it can delete the property, but trying to delete a variable declared with var that belongs to the global object is going to be false  

```js
  let obj = { x: 1, y: 2, z: 3 }; // object literal 
  delete o['x'] // => 1;
  'x' in obj // => false
```

## testing properties

- **in** evaluates to true if the key that you test is in that object, otherwise is going to be false

  ```JS
  const obj = { x: 1 };
  console.log('x' in obj);   //=> true there is a property with key name
  console.log('name' in obj); // false there isn't a property with key name
  ```

- **hasOwnProperty()** method of an object tests whether that object has an own property with the given name. It returns false for inherited properties:

  ```JS
  let obj1 = { x: 1 };
  let obj2 = Object.create(obj1);
  obj2.y = 2;
  console.log(obj2.hasOwnProperty('x')); //=> false, is an inherited property
  console.log(obj2.hasOwnProperty('y')); //=> true, is a property created in that object
  ```

- **propertyIsEnumerable()** refines the hasOwnProperty() test. It returns true only if the named property is an own property and its enumerable attribute is true. Certain built-in properties are not enumerable. Properties created by normal Java‐ Script code are enumerable unless you’ve used one of the techniques shown in §14.1 to make them non-enumerable.

```JS
console.log(obj2.hasOwnProperty('x')); //=> true, o has an own enumerable property x
console.log(obj2.hasOwnProperty('toLocaleString')); // // => false, not an own property
// To guard against enumerating inherited properties with for/in, you can add an explicit check inside the loop body: 
for(let p in o) {
   if (!o.hasOwnProperty(p)) continue; // Skip inherited properties 
}

for(let p in o) { if (typeof o[p] === "function") continue; // Skip all methods 
}
```

- **The ( !== )  operator** Instead of using the in operator, it is often sufficient to simply query the property and use !== to make sure it is not undefined:

 ```JS
 let o = { x: 1 }; o.x !== undefined // => true: o has a property x
 // there is one difference with the ( in ) tester 
 let o = { x: undefined }; // Property is explicitly set to undefined 
 o.x !== undefined // => false: property exists but is undefined 
 o.y !== undefined // => false: property doesn't even exist 
 "x" in o // => true: the property exists 
 "y" in o // => false: the property doesn't exist 
 delete o.x; // Delete the property x 
 "x" in o // => false: it doesn't exist anymore
 ```

## Extending Objects

- **Object.assign()** expects two or more objects as its arguments. It modifies and returns the first argument, which is the target object, but does not alter the second or any subsequent arguments, which are the source objects.

  ```JS
  const obj1 = {
  a: 1,
  b: 2,
  c: 3,
  };
  const obj2 = {
  d: 1,
  e: 2,
  a: 3,
  };
  Object.assign(obj1, obj2);
  console.log(obj1); //=> {a: 3, b: 2, c: 3, d: 1, e: 2}
  console.log(obj2); //=> {d: 1, e: 2, a: 3}
  // keep focus in object target
  const newObject = Object.assign(obj1, obj2);
  console.log('newObjecy => ',newObject); // => {a: 3, b: 2, c: 3, d: 1, e: 2} 
  console.log('obj1 => ',obj1); // => {a: 3, b: 2, c: 3, d: 1, e: 2}; still been the target object 1
  // Avoid side effects
  const newObject = Object.assign({}, obj1, obj2);
  console.log('newObjecy => ',newObject); // => {a: 3, b: 2, c: 3, d: 1, e: 2} 
  console.log('obj1 => ',obj1); // => {a: 1, b: 2, c: 3} has not been touch the target is {}
  // Using spread operator 
  const newObject = {...obj1, ...obj2};
  console.log('newObjecy => ',newObject); // => {a: 3, b: 2, c: 3, d: 1, e: 2}
  console.log('obj1 => ',obj1); // => {a: 1, b: 2, c: 3} has not been touch the target is {}
  // copies properties only if they are missing:
  function merge(target, ...sources) {
  for (let source of sources) {
    for (let key of Object.keys(source)) {
      if (!(key in target)) {
        // This is different than Object.assign()
        target[key] = source[key];
      }
    }
  }
  return target;
  }
  Object.assign({ x: 1 }, { x: 2, y: 2 }, { y: 3, z: 4 }); // => {x: 2, y: 3, z: 4}
  merge({ x: 1 }, { x: 2, y: 2 }, { y: 3, z: 4 }); // => {x: 1, y: 2, z: 4}
  ```

## Serializing Objects

 Object serialization is the process of converting an object’s state to a string from which it can later be restored. The functions JSON.stringify() and JSON.parse() serialize and restore JavaScript objects. These functions use the JSON data inter‐ change format. JSON stands for “JavaScript Object Notation,” and its syntax is very similar to that of JavaScript object and array literals:

  ```JS
  let o = {x: 1, y: {z: [false, null, ""]}}; // Define a test object let 
  s = JSON.stringify(o); // s == '{"x":1,"y":{"z":[false,null,""]}}' 
  let p = JSON.parse(s); // p == {x: 1, y: {z: [false, null, ""]}}
  ```

## The valueOf()

Method The valueOf() method is much like the toString() method, but it is called when JavaScript needs to convert an object to some primitive type other than a string— typically, a number. JavaScript calls this method automatically if an object is used in a context where a primitive value is required. The default valueOf() method does nothing interesting, but some of the built-in classes define their own valueOf() method. The Date class defines valueOf() to convert dates to numbers, and this allows Date objects to be chronologically compared with < and >. You could do some‐ thing similar with a point object, defining a valueOf() method that returns the dis‐ tance from the origin to the point:

  ```JS
  let point = {
  x: 3,
  y: 4,
  valueOf: function() { return Math.hypot(this.x, this.y); }
  }; 
  Number(point) // => 5: valueOf() is used for conversions to numbers 
  point > 4 // => true 
  point > 5 // => false 
  point < 6 // => true
  ```

## Shorthand Methods

  ```JS
  //normal syntax
  let square = {
    area: function() {return this.side * this.side; },
    side: 10
   };
  square.area() // => 100
  // Es6 new syntax
  let square = { 
    area() { return this.side * this.side; }, 
    "method With Spaces"(x) { return x + 1; }, 
    [METHOD_NAME](x) { return x + 2; },
    side: 10 
    }; 
  square.area() // => 100
  square["method With Spaces"](1) // => 2 
  square[METHOD_NAME](1) // => 3

