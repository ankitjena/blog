+++
title = "All the new awesome ES6 features"
date = 2018-11-02T13:23:10+01:00
draft = false
tags = ["es6", "Javascript"]
categories = []
+++

![](https://miro.medium.com/max/2048/1*0LH8jqFO1kZ0OVMhkKVF9g.jpeg)

JavaScript is the language of the web. Alongside HTML and CSS it is one of the three core technologies of the World Wide Web. It enables interactive web pages and thus is an essential part of almost every web application. Initially only implemented at the client-side in web browsers, JavaScript engines are embedded in many other types of host software, including server-side in web servers and databases, and in non-web programs such as word processors and PDF software, and in runtime environments that make JavaScript available for writing mobile and desktop applications, including desktop widgets.

So, what is ES6 (also known as ES2015). If you search about it on the web, I think the answers might not be able to feed your curious bug. So, [here’s a nice article by Micheal Aranda](https://medium.freecodecamp.org/whats-the-difference-between-javascript-and-ecmascript-cba48c73a2b5) that should answer your questions. Well, it did it for me.

ES6 was, so to say, the biggest update in which a lot of new features were added to JavaScript. Without wasting any time, let’s get into some of the major ones.

**let instead of var**

ES6 introduced the let keyword to us. let allows you to declare variables that are limited in scope to the block, statement, or expression on which it is used. This is unlike the var keyword, which defines a variable globally, or locally to an entire function regardless of block scope. An explanation of why the name let was chosen can be found [here](https://stackoverflow.com/questions/37916940/why-was-the-name-let-chosen-for-block-scoped-variable-declarations-in-javascri). Here’s an example.

```
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // same variable!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // different variable
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```

**Constants with the const keyword**
Constants are block-scoped, much like variables defined using the let statement. The value of a constant cannot change through reassignment, and it can't be redeclared.

```
const number = 42;try {
  number = 99;
} catch(err) {
  console.log(err);
  //expected output: TypeError: invalid assignment to const 'number'
  //Note - error messages will vary depending on browser
}console.log(number);
// expected output: 42
```

**Arrow functions**
An **arrow function expression** has a shorter syntax than a function expression and does not have its own [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this), [arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments), [super](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/super), or [new.target](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new.target). These function expressions are best suited for non-method functions, and they cannot be used as constructors.

Two factors influenced the introduction of arrow functions: shorter functions

```
var elements = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

//previous lengthy declaration
elements.map(function(element ) { 
  return element.length; 
}); // [8, 6, 7, 9]
//enter awesome arrow syntax
elements.map(element => {
  return element.length;
}); // [8, 6, 7, 9]

elements.map(element => element.length); // [8, 6, 7, 9]

elements.map(({ length }) => length); // [8, 6, 7, 9]
```

and no existence of *this* keyword.

```
function Person(){
  this.age = 0;

  setInterval(() => {
    this.age++; // |this| properly refers to the Person object
  }, 1000);
}

var p = new Person();
```

**Template Literals**

Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them.

Template literals are enclosed by the back-tick (` `)character instead of double or single quotes. Template literals can contain placeholders. These are indicated by the dollar sign and curly braces (${expression}). The expressions in the placeholders and the text between them get passed to a function. The default function just concatenates the parts into a single string.

```
var a = 5;
console.log('this' + a + 'is a number') //this 5 is a number
console.log(`this ${a} is a number`) //this 5 is a number
//for multiline strings
console.log('this is \na new line')
//using template literals
console.log(`this is a new line`)
```

**Rest parameter**

A function’s last parameter can be prefixed with ... which will cause all remaining (user supplied) arguments to be placed within a "standard" JavaScript array. Only the last parameter can be a "rest parameter".

```
function myFun(a, b, ...rest) {
  console.log("a", a); 
  console.log("b", b);
  console.log("Other arguments", rest); 
}

myFun("one", "two", "three", "four", "five", "six");

// Console Output:
// a, one
// b, two
// Other arguments, [three, four, five, six] 
```

**Spread Syntax**

Spread syntax according to me was the coolest feature of ES6. It allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected. Let’s take a look at examples to understand this better.

```
//using spread to pass arguments
function myFunction(x, y, z) {  
  console.log(x,y,z);
}
var args = [0, 1, 2];
myFunction(...args); //logs 0 1 2

//calling a constructor with new
var dateFields = [1970, 0, 1];  // 1 Jan 1970
var d = new Date(...dateFields); 

//create new array from existing array
var parts = ['shoulders', 'knees']; 
var lyrics = ['head', ...parts, 'and', 'toes'];

//copy and array
var arr = [1, 2, 3];
var arr2 = [...arr]; // like arr.slice()
arr2.push(4); 
// arr2 becomes [1, 2, 3, 4]
// arr remains unaffected

//concatenate arrays
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1 = [...arr1, ...arr2]; //[0, 1, 2, 3, 4, 5]

//using spread in object literals
var obj1 = { foo: 'bar', x: 42 };
var obj2 = { foo: 'baz', y: 13 };

var clonedObj = { ...obj1 };
// Object { foo: "bar", x: 42 }

var mergedObj = { ...obj1, ...obj2 };
// Object { foo: "baz", x: 42, y: 13 }
```

**Note**: Rest syntax looks exactly like spread syntax, but is used for destructuring arrays and objects. In a way, rest syntax is the opposite of spread syntax: spread ‘expands’ an array into its elements, while rest collects multiple elements and ‘condenses’ them into a single element.

**Classes and Inheritance**

JavaScript classes, introduced in ECMAScript 2015, are primarily syntactical sugar over JavaScript’s existing prototype-based inheritance. Previously defining classes in JavaScript would be a mundane task due to the prototype-based model. ES6 JavaScript made it simpler to declare classes and subsequently simpler inheritance protocols. This [link](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes) is a good source to get your concepts clear.

**Generator Functions**

Generators are functions which can be exited and later re-entered. Their context (variable bindings) will be saved across re-entrances.

Generators in JavaScript — especially when combined with Promises — are a very powerful tool for asynchronous programming as they mitigate — if not entirely eliminate — the problems with callbacks, such as Callback Hell and Inversion of Control.
This pattern is what `async` functions are built on top of.

Calling a generator function does not execute its body immediately; an iterator object for the function is returned instead. When the iterator’s `next()` method is called, the generator function's body is executed until the first `yield` expression, which specifies the value to be returned from the iterator or, with `yield*`, delegates to another generator function. The `next()` method returns an object with a `value` property containing the yielded value and a `done` property which indicates whether the generator has yielded its last value as a boolean. Calling the `next()` method with an argument will resume the generator function execution, replacing the yield expression where execution was paused with the argument from `next()`.

A `return` statement in a generator, when executed, will make the generator finished (i.e the `done` property of the object returned by it will be set to `true`). If a `value` is returned, it will be set as the value property of the object returned by the generator.
Much like a `return` statement, an error thrown inside the generator will make the generator finished -- unless caught within the generator's body.
When a generator is finished, subsequent `next` calls will not execute any of that generator's code, they will just return an object of this form: `{value: undefined, done: true}`.

```
//simple example
function* idMaker() {
  var index = 0;
  while (index < index+1)
    yield index++;
}

var gen = idMaker();

console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
// ...
```

### Other small features
**Default parameter values**

```
f = (x, y = 7, z = 42) => {     
     return x + y + z 
} 
f(1) === 50 //True
```

**Array Matching ,Swapping, Object Matching**

```
var list = [ 1, 2, 3 ] 
var [ a, , b ] = list //match a and b to 1 and 3

[ b, a ] = [ a, b ] //swap without using another variable

var { name, age, gender} = getDetails() //object matching
//instead of
var tmp = getDetails()
var name = tmp.name
var age = tmp.age
var gender = tmp.gender
```

These are the few features I thought are nice and will help you guys to write JavaScript better. Till the next one.