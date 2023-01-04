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

### More ES6 Goodness Coming Down The Pike!