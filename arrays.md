# Arrays

An array is an ordered list of element that has a number as position called index, arrays are mutable, can store any type of value the typeof is object

## There are five ways to create ana array:

1. **Arrays literals**: manual creation

2. **Array constructor**: you can create an empty array or an array with a length desired `let a = new Array(10);` give an sparse array with the length of 10.

3. **Array.of()**: allows you to create an array with a number value that not set the length of the array

4. **`Array.from(arrayToCopy, functionToLoweCase):`** you can copy other array and as second parameter you can pas a function to copy the elements modified.

5. **Spread operator** `[ . .  . arrayToCopy ]` you can copy an array and also you can insert the elements of one array inside of another array, also I can convert a string in a array

```js
  let a  = [ 1, 2, . . . arrayToCopy, 4, 5];
  let b = [ . . . “Hello”] // results will be [ “H”, “e”, “l”, “l”, “o”];
```

## Using **Set()** with _**spread operator**_

I can filter an array without adding the prototype of the function **Set**
  
```js
let a = [ . . .new Set (b)]; // a is now [ “H”, “e”, “l”, “o”];
```

## The _length_ property of the array

can be used to know the index number on the array, count also the spaces in a sparse array, you can also delete items fixing the length of an array or simply delete all the items.

```js
let b = [ . . . “Hello”] // => [ “H”, “e”, “l”, “l”, “o”]
b.length     // => the length is 5 
b.length = 3 // deletes the index 3, 4.
b.length = 0 // => [] delete the elements of the array
```

## Adding and deleting arrays elements

- **pop()** this method remove the last element of the array reducing the length and return the value.

```js
  let a = [...'Rafael']; // => ['R', 'a', 'f', 'a', 'e', 'l'] length of 6
  let arrayToPop = a.pop(); // => 'l';
  // a will be modified
  console.log(a) // => ['R', 'a', 'f', 'a', 'e'] length of 5
```

- **push** this method add one element at the end of the array is the same as assigning the value to a[a.length].

 ```js
  a.push(arrayToPop); // => ['R', 'a', 'f', 'a', 'e', 'l'] length of 6
 ```

- **shift** this method remove the first element of the array reducing the length, reorder de index and return the value.
  
 ```js  
  let arrayToShift = a.shift(); // => 'R';
  // a will be modified
  console.log(a) // => ['a', 'f', 'a', 'e', 'l'] length of 5
```

- **unshift()** this method add one element at the beginning of the array.

 ```js
  a.unshift(arrayToShift); // => ['R', 'a', 'f', 'a', 'e', 'l'] length of 6
 ```

- **splice** this method can add elements in any place of the array, add and remove at the same time or only remove, it works with 2 parameters the first is the position where is going to be inserted the element and the second the numbers of elements to delete starting from the index of the first parameter

 ```js

  let fruits = ['banana', 'fraise', 'apple', 'carrot', 'potato', 'grapes'];
  // add one fruit after fraise
  fruits.splice(2, 0, 'peach'); // => ['banana', 'fraise', 'peach', 'apple', 'carrot', 'potato' 'grapes'];
  // adding melon and after apple and delete carrot and potato
  fruits.splice(4, 2, 'melon'); // => ["banana", "fraise", "peach", "apple", "melon", "grapes"]
  // deleting at certain elements 
  let bigFruit =  fruits.splice(4,1); // => melon
  // fruits final status 
  console.log(fruits); // ["banana", "fraise", "peach", "apple", "grapes"]
  // delete all elements
  fruit.splice(0); // => []
 ```

- **slice** this method copy the elements desired in the array, uses two parameters, the first is the index where you want to start copying and the second the limiter index of the section you want to copy
  
```js
  let fruitsSliced =  fruits.slice(1, 4); // ["fraise", "peach", "apple"]
```

- **delete** this operator can delete an element of an array or the property of an objet _using this property in arrays do not alter the length of the array creating a sparse array_

```js
  let pets = ['dog', 'cat', 'bird', 'apple', 'rabbit'];
  delete pets[3];
  3 in pets // false, apple is not in the array
  pets.length // => 4
```

## Iterate  with arrays

Arrays like strings can use the same iterators could be a **for**-**for of**-**while**-**forEach method**

```js
  let nameLetters = [...'rafael']; // ['r', 'a', 'f', 'a', 'e', 'l']
  let name = '';
  // Using for of => 'rafael'
  for (let element of nameLetters) {
    name += element;
  }

  // accessing to keys with a entries() method
  let newArray = [];
  for (let [key, element]  of nameLetters.entries()) {
    //// letters at even indexes 
    if (index % 2 === 0)  {
      newArray.push(element);
    } 
  }

  // maintaining the array dense
  let denseArray = [];
  for (let element of nameLetters) {
    if (element !== undefined || element !== null) {
      denseArray.push(element);
    }
  }

  // accessing with a regular loop
  for (let i = 0; i < nameLetters.length; i++) {
    newArray.push(nameLetters[i]);
  }
```

## Create a multidimensional array

```js
let table = new Array(10); // 10 rows of the table
for (let i = 0; i < table.length; i++) {
  table[i] = new Array(10); // Each row has 10 columns
}
// Initialize the array
for (let row = 0; row < table.length; row++) {
  for (let col = 0; col < table[row].length; col++) {
    table[row][col] = row * col;
  }
}
// Use the multidimensional array to compute 5*7
console.log(table); // => 35
```

## Array methods

- **The forEach() method**
  The `forEach()` method iterates through an array, invoking a function you specify for each element. As described, you pass the function as the first argument to `forEach()`. `forEach()` then invokes your function with three arguments: the value of the array element, the index of the array element, and the array itself. If you only care about the value of the array element, you can write a function with only one parameter the additional arguments will be ignored:

```js
  let data = [1,2,3,4,5], sum = 0; // Compute the sum of the elements of the array 
  data.forEach(value => { sum += value; }); 
  console.log(sum); // sum = 15 // Now increment each array element
  data.forEach(function(v, i, a) { a[i] = v + 1; }); // data == [2,3,4,5,6]
  // Reverse strings
  let name = 'andres';
  let reversedUpperCased = '';
  [...name].reverse().forEach(letter => reversedUpperCased += letter.toUpperCase() );
  console.log(reversedUpperCased); // => SERDNA
```

- **The map() method**
  The `map()` method passes each element of the array on which it is invoked to the function you specify and returns an array containing the values returned by your function. Note that `map()` returns a new array: it does not modify the array it is invoked on. If that array is sparse, your function will not be called for the missing elements, but the returned array will be sparse in the same way as the original array: it will have the same length and the same missing elements. This method is very similar than `forEach()`.

```js
  let a = [1, 2, 3]; 
  a.map(x => x*x) // => [1, 4, 9]: the function takes input x and returns x*x
```

- **The filter() method**
  If the return value is true, or a value that converts to true, then the element passed to the predicate is a member of the subset and is added to the array that will become the return value.

```js
  let a = [5, 4, 3, 2, 1]; a.filter(x => x < 3) // => [2, 1]; values less than 3 
  a.filter((x,i) => i % 2 === 0) // => [5, 3, 1]; every other value
  let dense = sparse.filter(() => true); //To close the gaps in a sparse array,
  a = a.filter(x => x !== undefined && x !== null); //close gaps and remove undefined and null elements 
```

- **The find() method** this method stop iterating the first time the predicate finds an element. When that happens,  returns the matching element, if not matches fund
  find return undefined

```js
  let a = [1,2,3,4,5]; 
  a.find(x => x % 5 === 0) // => 5: this is a multiple of 5 
  a.find(x => x % 7 === 0) // => undefined: no multiples of 7 in the array
```

- **The findIndex() method** this method stop iterating the first time the predicate finds an element. When that happens,  returns the index of the element, if not matches fund findIndex return -1

```js
  let a = [1,2,3,4,5];
  a.findIndex(x => x === 3) // => 2; the value 3 appears at index 2
  a.findIndex(x => x < 0) // => -1; no negative numbers in the array
```

- **The every() method** returns true only if all the conditions of the value are true

```js
  let a = [1,2,3,4,5]; a.every(x => x < 10) // => true: all values are < 10. 
  a.every(x => x % 2 === 0) // => false: not all values are even.
```

- **The some() method** returns true only if at least one element is true otherwise returns false

```js
  let a = [1,2,3,4,5]; a.some(x => x % 2===0) // => true; a has some even numbers. 
  a.some(isNaN) // => false; a has no non-numbers.
```

- **The reduce() and reduceRight() methods**
  Combine the elements of an array, using the function you specify, to produce a single value. Takes two arguments the first is the accumulated result of the reduction, the second is the next value and as optional you can add an initializer, _Note: an empty array give typeError_

```js
  let a = [1,2,3,4,5];
  a.reduce((x,y) => x+y, 0) // => 15; the sum of the values 
  a.reduce((x,y) => x*y, 1) // => 120; the product of the values 
  a.reduce((x,y) => (x > y) ? x : y) // => 5; the largest of the values
  // reduceRight makes the same as reduce but from right to left
  let stringToSplit = [...'andres']
  let stringReversed = stringToSplit.reduceRight((x,y) => x+=y); // => 'serdna'
```

## Flattening arrays with flat() and flatMap() 

In ES2019, the flat() method creates and returns a new array that contains the same elements as the array it is called on, except that any elements that are themselves arrays are “flattened” into the returned array. For example:

```js
  [1, [2, 3]].flat() // => [1, 2, 3] 
  [1, [2, [3]]].flat() // => [1, 2, [3]]
  let a = [1, [2, [3, [4]]]]; 
  a.flat(1) // => [1, 2, [3, [4]]] 
  a.flat(2) // => [1, 2, 3, [4]] 
  a.flat(3) // => [1, 2, 3, 4] 
  a.flat(4) // => [1, 2, 3, 4]

```

The flatMap() method works just like the map() method (see “map()” on page 166) except that the returned array is automatically flattened as if passed to flat(). That is, calling a.flatMap(f) is the same as (but more efficient than) a.map(f).flat():

```js
  let phrases = ["hello world", "the definitive guide"]; 
  let words = phrases.flatMap(phrase => phrase.split(" "));
  words // => ["hello", "world", "the", "definitive", "guide"];
```

## Array Searching and Sorting Methods

- **indexOf() and lastIndexOf()** search an array for an element with a specified value and return the index of the first such element found, or -1 if none is found. indexOf() searches the array from beginning to end, and lastIndexOf() searches from end to beginning:

```js
  let a = [0,1,2,1,0]; 
  a.indexOf(1) // => 1: a[1] is 1 
  a.lastIndexOf(1) // => 3: a[3] is 1 
  a.indexOf(3) // => -1: no element has value 3
```

  indexOf() and lastIndexOf() compare their argument to the array elements using the equivalent of the === operator. If your array contains objects instead of primitive values, these methods check to see if two references both refer to exactly the same object. Use find() for objects

- **includes()** 
The ES2016 includes() method takes a single argument and returns true if the array contains that value or false otherwise. Is has a difference with lastIndex because it consider NaN equal to itself

```js
  let a = [1,true,3,NaN]; 
  a.includes(true) // => true 
  a.includes(2) // => false 
  a.includes(NaN) // => true 
  a.indexOf(NaN) // => -1; indexOf can't find NaN
```

- **sort()**
  sorts the elements of an array in place and returns the sorted array. When sort() is called with no arguments, it sorts the array elements in alphabetical order (temporarily converting them to strings to perform the comparison, if necessary): 
  
  ```js
  let a = ["banana", "cherry", "apple"]; 
  a.sort(); // a == ["apple", "banana", "cherry"]
  let a = [33, 4, 1111, 222]; a.sort(); // a == [1111, 222, 33, 4]; alphabetical order 
  a.sort((a,b) => a-b);// a == [4, 33, 222, 1111]; numerical order
  a.sort((a,b) => b-a); // a == [1111, 222, 33, 4]; reverse numerical order
  ```
