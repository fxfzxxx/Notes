# A re-introduction to JavaScript (JS tutorial)

> https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript

### Overview

- [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)
- [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- [`Boolean`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)
- [`Symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) (new in ES2015)
- `Object`
  - [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function)
  - [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
  - [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
  - [`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)
- [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)

### Numbers

No integer in JavaScript. In practice, integer values are treated as 32-bit ints, and some implementations even store it that way until they are asked to perform an instruction that's valid on a Number but not on a 32-bit integer. This can be important for bit-wise operations.

```javascript
parseInt('123', 10); // 123 
parseInt('010', 10); // 10
parseInt('010');  //  8 defaut in octal (radix 8)
parseInt('0x10'); // 16
parseInt('11', 2); // 3

/** You can also use the unary + operator to convert values to numbers: */
+ '42';   // 42
+ '010';  // 10
+ '0x10'; // 16

parseInt('hello', 10); // NaN
NaN + 5; // NaN
```

### Strings

They are sequences of UTF-16 code units; each code unit is represented by a 16-bit number. Each Unicode character is represented by either 1 or 2 code units.

```javascript
'hello'.length; // 5
'hello'.charAt(0); // "h"
'hello, world'.replace('world', 'mars'); // "hello, mars"
'hello'.toUpperCase(); // "HELLO"
```

### Other types

JavaScript distinguishes between [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null), which is a value that indicates a deliberate non-value (and is only accessible through the `null` keyword), and [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined), which is a value of type `undefined` that indicates an uninitialized variable — that is, a value hasn't even been assigned yet. We'll talk about variables later, but in JavaScript it is possible to declare a variable without assigning a value to it. If you do this, the variable's type is `undefined`. `undefined` is actually a **constant.**

### Variables

New variables in JavaScript are declared using one of three keywords: **`let`, `const`, or `var`**.

**`let`** allows you to declare block-level variables. 

**`const`** allows you to declare variables whose values are never intended to change. 

**`var`** is the most common declarative keyword. A variable declared with the **`var`** keyword is available from the *function* it is declared in.

```javascript
// myLetVariable is *not* visible out here

for (let myLetVariable = 0; myLetVariable < 5; myLetVariable++) {
  // myLetVariable is only visible in here
}

// myLetVariable is *not* visible out here

const Pi = 3.14; // variable Pi is set
Pi = 1; // will throw an error because you cannot change a constant variable.

// myVarVariable *is* visible out here

for (var myVarVariable = 0; myVarVariable < 5; myVarVariable++) {
  // myVarVariable is visible to the whole function
}

// myVarVariable *is* visible out here
```

### Operators

```javascript
123 == '123'; // true
1 == true; // true

123 === '123'; // false
1 === true;    // false
```

### Control Structure

Conditional statements are supported by `if` and `else`; you can chain them together if you like:

```java
var name = 'kittens';
if (name == 'puppies') {
  name += ' woof';
} else if (name == 'kittens') {
  name += ' meow';
} else {
  name += '!';
}
name == 'kittens meow';
```

JavaScript has `while` loops and `do-while` loops. 

```javascript
while (true) {
  // an infinite loop!
}

var input;
do {
  input = get_input();
} while (inputIsNotValid(input));
```

JavaScript's [`for` loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) is the same as that in C and Java: it lets you provide the control information for your loop on a single line.

```javascript
for (var i = 0; i < 5; i++) {
  // Will execute 5 times
}

for (let value of array) {
  // do something with value
}

for (let property in object) {
  // do something with object property
}
```

The `&&` and `||` operators use short-circuit logic, which means whether they will execute their second operand is dependent on the first. This is useful for checking for null objects before accessing their attributes:

```javascript
(var name = o) && (o.getName());

var name = cachedName || (cachedName = getName());

var allowed = (age > 18) ? 'yes' : 'no';

switch (action) {
  case 'draw':
    drawIt();
    break;
  case 'eat':
    eatIt();
    break;
  default:
    doNothing();
}
```

### Objects

The "name" part is a JavaScript string, while the value can be any JavaScript value — including more objects. This allows you to build data structures of arbitrary complexity.

There are two basic ways to create an empty object:

```javascript
var obj = new Object();
```

And:

```javascript
var obj = {};
```

Object literal syntax can be used to initialize an object in its entirety:

```javascript
var obj = {
  name: 'Carrot',
  _for: 'Max', // 'for' is a reserved word, use '_for' instead.
  details: {
    color: 'orange',
    size: 12
  }
};
```

Attribute access can be chained together:

```javascript
obj.detials.color; // orange
obj['details']['size']; // 12	
```

The following example creates an object **prototype**(`Person`) and an instance of that prototype(`you`).

```javascript
function Person(name,age){
    this.name = name;
    this.age = age;
}

// Define an object
var you = new Person('You',18);

```

**Once created**, an object's properties can again be accessed in one of two ways:

```javascript
you.name = 'newName';
var name = you.name;

you['name'] = 'newName';
var name = you['name'];
```

### Array

```javascript
var a = new Array();
a[0] = 'dog';
a[1] = 'cat';
a[2] = 'hen';
a.length; // 3

var a = ['dog', 'cat', 'hen'];
a.length; // 3
//If you query a non-existent array index, you'll get a value of undefined in return:
typeof a[90]; // undefined
```

If you take the above about `[]` and `length` into account, you can iterate over an array using the following `for` loop:

```javascript
for (var i = 0; i < a.length; i++) {
  // Do something with a[i]
}

for(const currentValue of a ){
    
}
```

Another way of iterating over an array that was added with ECMAScript 5 is `forEach()`:

```javascript
['dog','cat','hen'].foreach(function(currentValue,index,array){
    
})
```

More method:

| Method name                                          | Description                                                  |
| :--------------------------------------------------- | :----------------------------------------------------------- |
| `a.toString()`                                       | Returns a string with the `toString()` of each element separated by commas. |
| `a.toLocaleString()`                                 | Returns a string with the `toLocaleString()` of each element separated by commas. |
| `a.concat(item1[, item2[, ...[, itemN]]])`           | Returns a new array with the items added on to it.           |
| `a.join(sep)`                                        | Converts the array to a string — with values delimited by the `sep` param |
| `a.pop()`                                            | Removes and returns the last item.                           |
| `a.push(item1, ..., itemN)`                          | Appends items to the end of the array.                       |
| `a.shift()`                                          | Removes and returns the first item.                          |
| `a.unshift(item1[, item2[, ...[, itemN]]])`          | Prepends items to the start of the array.                    |
| `a.slice(start[, end])`                              | Returns a sub-array.                                         |
| `a.sort([cmpfn])`                                    | Takes an optional comparison function.                       |
| `a.splice(start, delcount[, item1[, ...[, itemN]]])` | Lets you modify an array by deleting a section and replacing it with more items. |
| `a.reverse()`                                        | Reverses the array.                                          |

### Functions

 The `return` statement can be used to return a value at any time, **terminating** the function. 

```javascript
function add(x, y) {
  var total = x + y;
  return total;
}
```

The **rest parameter operator** is used in function parameter lists with the format: **...variable** and it will include within that variable the entire list of uncaptured arguments that the function was called with. 

```javascript
function avg(...args){
    var sum = 0;
    for (let value of args){
        sum += value;
    }
    return sum/args.lenth;
}

avg(2,3,4); // 3
```

JavaScript lets you create anonymous functions.

```javascript
var avg = function(){
    var sum = 0;
    for(var i = 0; j = argument.length; i<j; i++){
        sum += argument[i];
    }
    return sum/ arguments.length;
        
}
```

This is semantically equivalent to the `function avg()` form. It's extremely powerful, as it lets you put a full function definition anywhere that you would normally put an expression. This enables all sorts of clever tricks. Here's a way of "hiding" some local variables — like block scope in C:

```javascript
var a = 1;
var b = 2;

(function() {
    var b = 3;
    var a+=b;
})();

a; //4
b; //2 is not chaneged but declared in the function
```

JavaScript allows you to call functions **recursively**. This is particularly useful for dealing with tree structures, such as those found in the browser DOM.

```javascript
function countChars(elm) {
    if(elm.nodeType ==3){//TEXT_NODE
        return elm.nodeValue.length;
    }
    var count = 0;
    for(var i = 0, child; child = elm.childNodes[i];i++){
        count += countChars(child);
    }
    return count;
}
```

This highlights a potential problem with anonymous functions: how do you call them recursively if they don't have a name? JavaScript lets you name function expressions for this. You can use named [IIFEs (Immediately Invoked Function Expressions)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE) as shown below:

```javascript
var charsInBody = (function counter(elm){
    if(elm.nodeType ==3){//TEXT_NODE
        return elm.nodeValue.length;
    }
    var count = 0;
    for(var i = 0, child; child = elm.childNodes[i];i++){
        count += countChars(child);
    }
    return count;
})
```

The name provided to a function expression as above is only available to the function's own scope. This allows more optimizations to be done by the engine and results in more readable code. The name also shows up in the debugger and some stack traces, which can save you time when debugging.



### Custom objects

JavaScript is a prototype-based language that contains no class statement, as you'd find in C++ or Java (this is sometimes confusing for programmers accustomed to languages with a class statement). Instead, JavaScript uses functions as classes. 

```javascript
function makePerson(firstmlast){
    return{
    	first:first,
    	last:last,
    	fullName: function(){
        	return this.last + this.first;
    	},
    };
}

var s = makePerson('John','Wick');
s.fullName();
```

Improved with **`this`** keyword:

```javascript
function Person(first, last) {
  this.first = first;
  this.last = last;
  this.fullName = function() {
    return this.first + ' ' + this.last;
  };
  this.fullNameReversed = function() {
    return this.last + ', ' + this.first;
  };
}
var s = new Person('Simon', 'Willison');
```

Our person objects are getting better, but there are still some ugly edges to them. Every time we create a person object we are creating two brand new function objects within it — wouldn't it be better if this code was shared?

```javascript
function personFullName() {
  return this.first + ' ' + this.last;
}
function personFullNameReversed() {
  return this.last + ', ' + this.first;
}
function Person(first, last) {
  this.first = first;
  this.last = last;
  this.fullName = personFullName;
  this.fullNameReversed = personFullNameReversed;
}
```

`Person.prototype` is an object shared by all instances of `Person`. It forms part of a lookup chain (that has a special name, "prototype chain"): any time you attempt to access a property of `Person` that isn't set, JavaScript will check `Person.prototype` to see if that property exists there instead. As a result, anything assigned to `Person.prototype` becomes available to all instances of that constructor via the `this` object.

This is an incredibly powerful tool. JavaScript lets you modify something's prototype at any time in your program, which means you can add extra methods to existing objects at runtime:

```javascript
function Person(first,last){
    this.first = first;
    this.last = last;
}
Person.prototype.fullname = function(){
    return this.first + this.last;
}

var s = new Person('Simon', 'Willison');
s.firstNameCaps(); // TypeError on line 1: s.firstNameCaps is not a function

Person.prototype.firstNameCaps = function() {
  return this.first.toUpperCase();
};
s.firstNameCaps(); // "SIMON"
```

Interestingly, you can also add things to the prototype of built-in JavaScript objects. Let's add a method to `String` that returns that string in reverse:

```javascript
var s = 'Simon';
s.reversed(); // TypeError on line 1: s.reversed is not a function

String.prototype.reversed = function() {
  var r = '';
  for (var i = this.length - 1; i >= 0; i--) {
    r += this[i];
  }
  return r;
};

s.reversed(); // nomiS
```

Remember how `avg.apply()` had a null first argument? We can revisit that now. The first argument to `apply()` is the object that should be treated as '`this`'. For example, here's a trivial implementation of `new`:

```javascript
function trivialNew(constructor, ...args) {
  var o = {}; // Create an object
  constructor.apply(o, args);
  return o;
}
```

This isn't an exact replica of `new` as it doesn't set up the prototype chain (it would be difficult to illustrate). This is not something you use very often, but it's useful to know about. In this snippet, `...args` (including the ellipsis) is called the "[rest arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)" — as the name implies, this contains the rest of the arguments.

Calling

```javascript
var bill = trivialNew(Person, 'William', 'Orange');
```

is therefore almost equivalent to

```javascript
var bill = new Person('William', 'Orange');
```

`apply()` has a sister function named [`call`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), which again lets you set `this` but takes an expanded argument list as opposed to an array.

```javascript
function lastNameCaps() {
  return this.last.toUpperCase();
}
var s = new Person('Simon', 'Willison');
lastNameCaps.call(s);
// Is the same as:
s.lastNameCaps = lastNameCaps;
s.lastNameCaps(); // WILLISON
```

### Inner functions

An important detail of nested functions in JavaScript is that they can access variables in their parent function's scope:

```javascript
function parentFunc() {
  var a = 1;

  function nestedFunc() {
    var b = 4; // parentFunc can't use this
    return a + b;
  }
  return nestedFunc(); // 5
}
```

This provides a great deal of utility in writing more maintainable code. If a called function relies on one or two other functions that are not useful to any other part of your code, you can nest those utility functions inside it. This keeps the number of functions that are in the global scope down, which is always a good thing.

This is also a great counter to the lure of global variables. When writing complex code it is often tempting to use global variables to share values between multiple functions — which leads to code that is hard to maintain. Nested functions can share variables in their parent, so you can use that mechanism to couple functions together when it makes sense without polluting your global namespace — "local globals" if you like. This technique should be used with caution, but it's a useful ability to have.

### Closures

This leads us to one of the most powerful abstractions that JavaScript has to offer — but also the most potentially confusing. What does this do?

```javascript
function makeAdder(a) {
  return function(b) {
    return a + b;
  };
}
var add5 = makeAdder(5);
var add20 = makeAdder(20);
add5(6); // ?
add20(7); // ?
```

The name of the `makeAdder()` function should give it away: it creates new 'adder' functions, each of which, when called with one argument, adds it to the argument that it was created with.

What's happening here is pretty much the same as was happening with the inner functions earlier on: a function defined inside another function has access to the outer function's variables. The only difference here is that the outer function has returned, and hence common sense would seem to dictate that its local variables no longer exist. But they *do* still exist — otherwise, the adder functions would be unable to work. What's more, there are two different "copies" of `makeAdder()`'s local variables — one in which `a` is 5 and the other one where `a` is 20. So the result of that function calls is as follows:

```javascript
add5(6); // returns 11
add20(7); // returns 27
```

Here's what's actually happening. Whenever JavaScript executes a function, a 'scope' object is created to hold the local variables created within that function. It is initialized with any variables passed in as function parameters. This is similar to the global object that all global variables and functions live in, but with a couple of important differences: firstly, a brand new scope object is created every time a function starts executing, and secondly, unlike the global object (which is accessible as `this` and in browsers as `window`) these scope objects cannot be directly accessed from your JavaScript code. There is no mechanism for iterating over the properties of the current scope object, for example.

So when `makeAdder()` is called, a scope object is created with one property: `a`, which is the argument passed to the `makeAdder()` function. `makeAdder()` then returns a newly created function. Normally JavaScript's garbage collector would clean up the scope object created for `makeAdder()` at this point, but the returned function maintains a reference back to that scope object. As a result, the scope object will not be garbage-collected until there are no more references to the function object that `makeAdder()` returned.

Scope objects form a chain called the scope chain, similar to the prototype chain used by JavaScript's object system.

A **closure** is the combination of a function and the scope object in which it was created. Closures let you save state — as such, they can often be used in place of objects. You can find [several excellent introductions to closures](http://stackoverflow.com/questions/111102/how-do-javascript-closures-work).