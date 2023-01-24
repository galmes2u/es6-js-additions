# ES6 Code Descriptions and Samples

As we discussed in class, ECMAScript6 introduced many important additions to the Javascript language. It's important to know that these changes don't create any capabilities that didn't exist before, but they provided a more efficient way of performing those operations.

Code which improves the overall "look" of a process without changing it fundamentally is often called *syntactic sugar*. It's a good phrase to throw out there during job interviews.

So far we have discussed:
<br><br>

---
## Const and Let
---

Const and let give us more precision in how we declare variables.

`let` is the easiest. Any variable created with let can have its value changed anytime, as well as having the entire variable re-assigned to something completely new.

`const` makes any variable represemting a primitive value (string, number, boolean) *immutable* (another good word). This means it cannot be changed anywhere else in the code.

For complex data types. `const` allows you to mutate within the array or object, but you cannot re-assign the actual array or object to something else.

Examples:

```
   let title = "President";
   title = "Bottle Washer";   // allowed

   const salary = 120000;
   salary = 150000;           // not allowed

   const user = {
    name: "Bob",
    email: "bob@gmail.com"
   }
   
   user.email = bob2@gmail.com   // allowed
   user = "Bob";                 // not allowed
```

<br>

---
## Arrow Functions
---

Arrow functions are a "shorthand" way of writing simple functions. 

Given this function:

```
   function reverseMyName(name){
    return name.split("").reverse().join("")
   }
```

You can rewrite it as an arrow function as follows:

``` const reverseMyName = name => name.split("").reverse().join("") ``` 

Key points regarding arrow functions:

- When the function contains only a single expression, you can omit the curly braces and the "return" operator. These are implied. But for functions with more code inside them, you would use the curly braces and the "return" operator as per usual.
- If only one argument is passed into an arrow function, that argument does not need to be wrapped inside parenthesis.
- If no arguments, or more than one argument, are passed, parenthesis must be used.
- Arrow functions are scoped differently than "standard" functions. Most of the time, this doesn't matter. But an arrow function is always scoped to the scope possessed by it's creator. So we can't use arrow functions as object methods. Example:

```
const myObj = {
  name: "Joe",
  age: 27,
  sayHappyBirthday: function(){
    console.log("Happy birthday, " + this.name)
  }
}

myObj.sayHappyBirthday();   // returns "Happy Birthday, Joe"
```

"Standard" functions are scoped to wherever they are created. Here, sayHappyBirthday inherits its scope from the myObj object.

Now consider this:

```
const myObj = {
  name: "Joe",
  age: 27,
  sayHappyBirthday: () => console.log("Happy birthday, " + this.name)
}

myObj.sayHappyBirthday();   // returns "Happy birthday, undefined"
```

This fails, because arrow functions are scoped to where they are **invoked**. Here we call `sayHappyBirthday()` from the global scope (outside of the myObj object), so that's where the arrow function looks for a variable called "name".

<br>

---
## The forEach() Method
---

The forEach method is built into every array generated in Javascript, and provides an easy way to iterate over all elements in an array. The method simply needs a callback function where you indicate what operation(s) to perform on each array member. This callback function can receive two arguments: a variable identifier for each member of the array, and (optional) a variable identifier for the index position of each item.

Example:

```
const myArr = [ "Bob", "Sue", "Henry" ];
myArr.forEach( (name, idx) => {
  console.log(name + " is at idx position " + idx)
})

```


<br>

---
## Array Filter and Find
---

These two methods make it easy to extract specific elements from an array. Both accept a callback function where you specify the criteria for the array members you are seeking.

The filter() returns an array of all matching members. The find() returns only the first match.

For instance, given this array:

```
const myArr = [
  { id: 1, name: "Bob", age: 30 },
  { id: 2, name: "Mary", age: 20 },
  { id: 3, name: "Sue", age: 40 },
  { id: 4, name: "Dan", age: 35 }
]
```

If I want to find all possible members who are older than 30:

```
const olderThan30 = myArr.filter( person => person.age > 30 )
```

If I want to find the member named Sue:

```
const whereIsSue = myArr.find( person => person.name === "Sue" )
```


<br>

---
## Array Mapping
---

Array Mapping transforms one array into another. It is called on a target array, but does not mutate that array. Instead, it returns a new array with the modified members. When array mapping, the new array must have the same number of members as the target array, but these members can be modified in any way.

The map() function accepts a callback, where we specify what operation(s) to perform during the map.

In this example, we take an array of people objects, and map it into an array of just their names:

```
const arrOfPeople = [ { id: 1, name: "Bob", age: 30 }, { id: 2, name: "Mary", age: 20 } ];
const arrOfNames = arrOfPeople.map( person => person.name );
```



<br>

---
## The Rest Operator
---

The Rest Operator takes any number of comma-separated elements and essentially merges them into an array. It's used often in functions when the number of arguments that can be provided is not a defined amount.

For instance:

```
function addTheseNumbers(...nums){
  let sum = 0;
  nums.forEach( num => sum = sum + num )
  return sum
}

console.log( addTheseNumbers(1,2,4) );  // 7
console.log( addTheseNumbers(10,20,30,40,100) );  // 200
```

Here we have a function called addTheseNumbers, which we want to work no matter how many actual numbers are passed into it.


<br>

---
## The Spread Operator
---

The spread operator is used when you want to extract the members of an object or an array into their discrete elements.

Example:

```
const group1 = [ "Bob", "Sue", "Henry" ];
const group2 = [ "Ralph", "Agnes", "Dee" ];
const combined = [...group1, ...group2];

console.log(combined);  // ["Bob", "Sue", "Henry", "Ralph", "Agnes", "Dee"]
```

In the example above, the spread operator pulls out the elements of each array so that they can be joined into a new array.




### More ES6 Goodness Coming Down The Pike!