# Angular and JavaScript Fundamentals

This README provides a comprehensive overview of Angular and JavaScript, two fundamental technologies in web development. It covers their definitions, key features, and practical examples to help you understand their core concepts, including advanced topics relevant for interviews.

## 1. JavaScript

### Definition

JavaScript (JS) is a high-level, interpreted scripting language primarily used for creating interactive and dynamic content on web pages. It is a core technology of the World Wide Web, alongside HTML and CSS, and is supported by all modern web browsers. Beyond browsers, JavaScript is also used in server-side programming (Node.js), mobile app development (React Native), and desktop applications (Electron).

### Key Concepts and Examples

#### 1.1 Variable Declarations (var, let, const)

JavaScript has three types of variable declarations:

- **var**: Function-scoped, traditionally used. Variables declared with var are hoisted to the top of their function or global scope.
- **let**: Block-scoped, introduced in ES6 (ECMAScript 2015). Variables declared with let are hoisted but not initialized, leading to a "temporal dead zone."
- **const**: Block-scoped constant, introduced in ES6. Variables declared with const must be initialized at declaration and cannot be reassigned. Like let, they are block-scoped and have a temporal dead zone.

Example:

```javascript
// var example
var x = 10;
if (true) {
  var x = 20; // Same variable, re-declared and reassigned
  console.log('Inside block (var x):', x); // Output: Inside block (var x): 20
}
console.log('Outside block (var x):', x); // Output: Outside block (var x): 20 (var is function-scoped)

// let example
let y = 20;
if (true) {
  let y = 30; // Different variable, block-scoped
  console.log('Inside block (let y):', y); // Output: Inside block (let y): 30
}
console.log('Outside block (let y):', y); // Output: Outside block (let y): 20

// const example
const z = 30;
// const z = 40; // Error: Identifier 'z' has already been declared
// z = 40;     // Error: Assignment to constant variable.
console.log('const z:', z); // Output: const z: 30
```


#### 1.2 Functions and Scope

- **Functions**: Blocks of code designed to perform a particular task. They can take parameters and return values.
- **Scope**: Determines the accessibility of variables, objects, and functions from different parts of the code. JavaScript has global scope, function scope (for var), and block scope (for let and const).

Example:

```javascript
let globalVar = 'I am global'; // Global scope

function outerFunction() {
  let outerVar = 'I am in outer function'; // Function scope

  function innerFunction() {
    let innerVar = 'I am in inner function'; // Function scope
    console.log(globalVar);   // Accessible
    console.log(outerVar);    // Accessible
    console.log(innerVar);    // Accessible
  }

  innerFunction();
  // console.log(innerVar); // Error: innerVar is not defined (out of scope)
}

outerFunction();
// console.log(outerVar); // Error: outerVar is not defined (out of scope)
```


#### 1.3 Closures

A closure is a combination of a function and the lexical environment within which that function was declared. This allows the function to retain access to variables from its parent scope even after the parent function has finished executing.

Example:

```javascript
function makeCounter() {
  let count = 0; // 'count' is in the lexical environment of makeCounter
  return function() { // This inner function forms a closure
    count++;
    return count;
  };
}

let counter1 = makeCounter();
console.log(counter1());  // Output: 1
console.log(counter1());  // Output: 2

let counter2 = makeCounter(); // Creates a new closure with its own 'count'
console.log(counter2());  // Output: 1
console.log(counter1());  // Output: 3 (counter1's count is independent)
```


#### 1.4 Hoisting

Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope during the compilation phase, before code execution. This means you can use variables and functions before they are declared in the code. However, only declarations are hoisted, not initializations.

Example:

```javascript
console.log(hoistedVar); // Output: undefined (declaration is hoisted, initialization is not)
var hoistedVar = 'I am hoisted';
console.log(hoistedVar); // Output: I am hoisted

hoistedFunction(); // Output: I am a hoisted function!
function hoistedFunction() {
  console.log('I am a hoisted function!');
}

// console.log(letVar); // Error: Cannot access 'letVar' before initialization (Temporal Dead Zone)
let letVar = 'I am let';
```


#### 1.5 Currying

Currying is a transformation of functions that translates a function from callable as f(a, b, c) into callable as f(a)(b)(c). It's a technique of breaking down a function that takes multiple arguments into a series of functions that each take a single argument.

Example:

```javascript
function SumOfThee(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

console.log(SumOfThee(2)(3)(4));  // Output: 9

// Another example for reusability
const addTwo = SumOfThee(2);
const addTwoAndThree = addTwo(3);
console.log(addTwoAndThree(5)); // Output: 10 (2 + 3 + 5)
```


#### 1.6 Difference between == and === operators

- The == (equality) operator checks for equality, but it performs type coercion if the operands are of different types. It attempts to convert the operands to a common type before comparison.
- The === (strict equality) operator checks for equality without performing type coercion, meaning both value and type must be the same for it to return true.

Example:

```javascript
console.log(5 == '5');   // Output: true (type coercion: string '5' becomes number 5)
console.log(5 === '5');  // Output: false (different types: number vs string)
console.log(0 == false); // Output: true (type coercion: false becomes 0)
console.log(0 === false);// Output: false (different types: number vs boolean)
console.log(null == undefined); // Output: true (special case for loose equality)
console.log(null === undefined); // Output: false
```


#### 1.7 Built-in Array Methods

JavaScript provides several built-in methods for manipulating arrays. Some of these methods include:

- push(): Adds one or more elements to the end of an array and returns the new length.
- pop(): Removes the last element from an array and returns that element.
- shift(): Removes the first element from an array and returns that element.
- unshift(): Adds one or more elements to the beginning of an array and returns the new length.
- splice(): Changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
- slice(): Returns a shallow copy of a portion of an array into a new array object.
- concat(): Used to merge two or more arrays. This method does not change the existing arrays, but instead returns a new array.
- forEach(): Executes a provided function once for each array element.
- map(): Creates a new array populated with the results of calling a provided function on every element in the calling array.
- filter(): Creates a new array with all elements that pass the test implemented by the provided function.
- reduce(): Executes a reducer function on each element of the array, resulting in a single output value.

Example:

```javascript
const fruits = ['apple', 'banana', 'cherry'];

fruits.push('date');        // fruits: ['apple', 'banana', 'cherry', 'date']
console.log('After push:', fruits);

const lastFruit = fruits.pop(); // lastFruit: 'date', fruits: ['apple', 'banana', 'cherry']
console.log('After pop:', fruits, 'Removed:', lastFruit);

const newFruits = fruits.map(fruit => fruit.toUpperCase()); // newFruits: ['APPLE', 'BANANA', 'CHERRY']
console.log('After map:', newFruits);

const filteredFruits = fruits.filter(fruit => fruit.length > 5); // filteredFruits: ['banana', 'cherry']
console.log('After filter:', filteredFruits);

const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, current) => acc + current, 0); // sum: 15
console.log('Sum using reduce:', sum);
```


#### 1.8 The Event Loop (Call Stack, Microtask, Macrotask)

The Event Loop is a fundamental concept in JavaScript's concurrency model. It allows JavaScript to perform non-blocking I/O operations despite being single-threaded.

- **Call Stack**: A LIFO (Last In, First Out) stack that stores function calls. When a function is called, it's pushed onto the stack. When it returns, it's popped off.
- **Web APIs**: Browser-provided APIs (e.g., setTimeout, fetch, DOM events) that handle asynchronous operations.
- **Callback Queue (Macrotask Queue)**: Stores callbacks from Web APIs (like setTimeout, setInterval, I/O operations, UI rendering).
- **Microtask Queue**: Stores callbacks for Promises (.then(), .catch(), .finally()) and queueMicrotask(). The microtask queue has higher priority than the macrotask queue.
- **Event Loop**: Continuously monitors the Call Stack and the queues. If the Call Stack is empty, it first checks the Microtask Queue. If there are tasks, it moves them to the Call Stack. Once the Microtask Queue is empty, it moves one task from the Callback Queue to the Call Stack.

Example (Conceptual):

```javascript
console.log('1. Start'); // Sync, goes to Call Stack, executes immediately

setTimeout(() => {
  console.log('4. setTimeout callback (Macrotask)'); // Goes to Web API, then Macrotask Queue
}, 0);

Promise.resolve().then(() => {
  console.log('3. Promise callback (Microtask)'); // Goes to Microtask Queue
});

console.log('2. End'); // Sync, goes to Call Stack, executes immediately

// Expected Output:
// 1. Start
// 2. End
// 3. Promise callback (Microtask)
// 4. setTimeout callback (Macrotask)
```


#### 1.9 Prototypes, Prototype Chain, and Prototypal Inheritance

- **Prototypes**: In JavaScript, every object has a prototype object from which it inherits properties and methods. This prototype object can also have its own prototype, and so on, forming a chain.
- **Prototype Chain**: The series of links between objects and their prototypes. When you try to access a property or method on an object, JavaScript first looks on the object itself. If not found, it looks on its prototype, then its prototype's prototype, and so on, until it reaches null.
- **Prototypal Inheritance**: The mechanism by which JavaScript objects inherit features from one another. It's a core concept of JavaScript's object-oriented nature.

Example:

```javascript
const animal = {
  eats: true,
  walk() {
    console.log('Animal walks');
  }
};

const rabbit = {
  jumps: true,
  __proto__: animal // rabbit inherits from animal
};

const longEar = {
  earLength: 10,
  __proto__: rabbit // longEar inherits from rabbit (and transitively from animal)
};

console.log(rabbit.eats);     // Output: true (inherited from animal)
rabbit.walk();                // Output: Animal walks (inherited from animal)
console.log(longEar.jumps);   // Output: true (inherited from rabbit)
longEar.walk();               // Output: Animal walks (inherited from animal)
```


#### 1.10 Callbacks

A callback is a function passed as an argument to another function, which is then executed inside the outer function at a later point in time. Callbacks are a fundamental pattern for handling asynchronous operations in JavaScript before Promises and async/await.

Example:

```javascript
function fetchData(callback) {
  console.log('Fetching data...');
  setTimeout(() => {
    const data = { id: 1, name: 'Sample Data' };
    callback(data); // Execute the callback with the fetched data
  }, 2000); // Simulate 2-second delay
}

function processData(data) {
  console.log('Data received:', data);
  console.log('Processing data...');
}

fetchData(processData); // Pass processData as a callback
console.log('Request sent, waiting for data...');
```


#### 1.11 Asynchronous JavaScript (Promises, async/await)

Asynchronous JavaScript allows operations to run in the background without blocking the main execution thread.

- **Promises**: An object representing the eventual completion or failure of an asynchronous operation and its resulting value. A Promise can be in one of three states: pending, fulfilled (resolved), or rejected.
- **async/await**: Syntactic sugar built on top of Promises, making asynchronous code look and behave more like synchronous code. async functions always return a Promise, and await pauses the execution of an async function until a Promise settles.

Example (Promises):

```javascript
function simulateAsyncOperation(success) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (success) {
        resolve('Operation successful!');
      } else {
        reject('Operation failed!');
      }
    }, 1500);
  });
}

simulateAsyncOperation(true)
  .then(message => {
    console.log('Promise resolved:', message);
  })
  .catch(error => {
    console.error('Promise rejected:', error);
  });

simulateAsyncOperation(false)
  .then(message => {
    console.log('Promise resolved:', message);
  })
  .catch(error => {
    console.error('Promise rejected:', error);
  });
```

Example (async/await):

```javascript
async function performAsyncOperation() {
  try {
    console.log('Starting async operation...');
    const result = await simulateAsyncOperation(true); // Await the promise to resolve
    console.log('Async/await success:', result);

    const failedResult = await simulateAsyncOperation(false); // This will throw an error
    console.log('This line will not be reached:', failedResult);
  } catch (error) {
    console.error('Async/await error caught:', error);
  }
}

performAsyncOperation();
```


#### 1.12 Promise Methods

Promise methods are fundamental to asynchronous JavaScript programming, providing a way to handle asynchronous operations and their results.

- **Promise.resolve()**: Returns a Promise object that is resolved with a given value. Commonly used to convert non-Promise values into Promise objects.
- **Promise.reject()**: Returns a Promise object that is rejected with a given reason (typically an Error object). Useful for signaling that an asynchronous operation has failed.
- **Promise.all()**: Takes an iterable of Promises as input and returns a single Promise that resolves when all of the input Promises have resolved, or rejects if any of the input Promises reject. Useful for concurrent operations.
- **Promise.race()**: Takes an iterable of Promises and returns a Promise that resolves or rejects as soon as one of the input Promises resolves or rejects, with the value or reason from that Promise. Useful for responding to the fastest operation.

Example:

```javascript
const p1 = new Promise(resolve => setTimeout(() => resolve('P1 resolved'), 1000));
const p2 = new Promise(resolve => setTimeout(() => resolve('P2 resolved'), 500));
const p3 = new Promise((_, reject) => setTimeout(() => reject('P3 rejected'), 700));

// Promise.all
Promise.all([p1, p2])
  .then(results => console.log('Promise.all results:', results)) // Output: ['P1 resolved', 'P2 resolved'] (after 1 second)
  .catch(error => console.error('Promise.all error:', error));

Promise.all([p1, p3])
  .then(results => console.log('Promise.all results (with reject):', results))
  .catch(error => console.error('Promise.all error (with reject):', error)); // Output: P3 rejected (after 0.7 seconds)

// Promise.race
Promise.race([p1, p2])
  .then(result => console.log('Promise.race result:', result)) // Output: P2 resolved (after 0.5 seconds)
  .catch(error => console.error('Promise.race error:', error));

Promise.race([p1, p3])
  .then(result => console.log('Promise.race result (with reject):', result))
  .catch(error => console.error('Promise.race error (with reject):', error)); // Output: P3 rejected (after 0.7 seconds)
```


#### 1.13 call, apply, and bind

These methods are used to control the this context of a function.

- **call()**: Invokes a function with a given this value and arguments provided individually.
- **apply()**: Invokes a function with a given this value and arguments provided as an array (or an array-like object).
- **bind()**: Returns a new function, allowing you to set the this context for any future calls to that function. It does not immediately execute the function.

Example:

```javascript
const person = {
  name: 'Alice',
  greet: function(city, country) {
    console.log(`Hello, my name is ${this.name} and I am from ${city}, ${country}.`);
  }
};

const anotherPerson = {
  name: 'Bob'
};

// Using call() - arguments are passed individually
person.greet.call(anotherPerson, 'New York', 'USA'); // Output: Hello, my name is Bob and I am from New York, USA.

// Using apply() - arguments are passed as an array
person.greet.apply(anotherPerson, ['London', 'UK']); // Output: Hello, my name is Bob and I am from London, UK.

// Using bind() - returns a new function
const greetBob = person.greet.bind(anotherPerson, 'Paris');
greetBob('France'); // Output: Hello, my name is Bob and I am from Paris, France.
```


#### 1.14 this in JavaScript

The this keyword in JavaScript refers to the context in which a function is executed. Its value depends on how the function is called:

- Global context: this refers to the global object (e.g., window in browsers, global in Node.js).
- Method context: If a function is called as a method of an object, this refers to that object.
- Constructor context: When a function is used as a constructor with new, this refers to the newly created instance.
- Explicit binding: Using call(), apply(), or bind() allows you to explicitly set this.
- Arrow functions: Arrow functions do not have their own this context; they inherit this from their lexical (enclosing) scope.

Example:

```javascript
// Global context
console.log(this === window); // In browser: true

// Method context
const obj = {
  name: 'Object A',
  logName: function() {
    console.log(this.name);
  }
};
obj.logName(); // Output: Object A

// Constructor context
function Car(make) {
  this.make = make;
}
const myCar = new Car('Toyota');
console.log(myCar.make); // Output: Toyota

// Arrow function context
const arrowObj = {
  name: 'Arrow Object',
  logNameArrow: () => {
    console.log(this.name); // 'this' here refers to the global object (window/global)
  },
  logNameRegular: function() {
    // 'this' here refers to arrowObj
    const innerArrow = () => {
      console.log(this.name); // 'this' here correctly refers to arrowObj
    };
    innerArrow();
  }
};
arrowObj.logNameArrow(); // In browser: undefined (or empty string depending on strict mode)
arrowObj.logNameRegular(); // Output: Arrow Object
```


#### 1.15 Document Object Model (DOM)

The Document Object Model (DOM) is a programming interface for HTML and XML documents. It represents the page structure as a tree of objects, where each node represents a part of the document (e.g., element, attribute, text). The DOM provides a way for JavaScript to interact with and manipulate the content, structure, and style of a web page.

Example (Conceptual):

```html
<!-- HTML Structure -->
<div id="container">
  <p class="text">Hello, <span id="name">World</span>!</p>
  <button id="changeTextBtn">Change Text</button>
</div>

<script>
  // Accessing DOM elements
  const container = document.getElementById('container');
  const nameSpan = document.getElementById('name');
  const button = document.getElementById('changeTextBtn');

  // Modifying content
  nameSpan.textContent = 'JavaScript';

  // Adding event listener
  button.addEventListener('click', () => {
    const paragraph = container.querySelector('.text');
    paragraph.style.color = 'blue';
    paragraph.style.fontWeight = 'bold';
    console.log('Text color changed!');
  });
</script>
```


#### 1.16 Template Literals, Destructuring, Spread Operator, and Rest Operator

These are powerful ES6+ features that enhance code readability and conciseness.

- **Template Literals**: Backtick-enclosed string literals (``) that allow for embedded expressions (\${expression}) and multi-line strings without special characters.
- **Destructuring Assignment**: A syntax that allows you to unpack values from arrays or properties from objects into distinct variables.
- **Spread Operator (...)**: Expands an iterable (like an array or string) into individual elements or an object into key-value pairs. Useful for copying arrays/objects, concatenating, or passing arguments.
- **Rest Operator (...)**: Collects an indefinite number of arguments into an array. Used in function parameters.

Example:

```javascript
// Template Literals
const userName = 'Alice';
const greeting = `Hello, ${userName}!
Welcome to the multi-line world.`;
console.log(greeting);

// Destructuring arrays
const numbers = [1, 2, 3];
const [a, b, c] = numbers;
console.log('Array Destructuring:', a, b, c); // Output: 1 2 3

// Destructuring objects
const person = { name: 'Alice', age: 30, city: 'London' };
const { name, age } = person; // Extracts 'name' and 'age'
console.log('Object Destructuring:', name, age); // Output: Alice 30

// Spread operator (for arrays)
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // Creates a new array by spreading arr1
console.log('Spread Array:', arr2); // Output: [1, 2, 3, 4, 5]

// Spread operator (for objects)
const obj1 = { x: 1, y: 2 };
const obj2 = { ...obj1, z: 3 }; // Creates a new object by spreading obj1
console.log('Spread Object:', obj2); // Output: { x: 1, y: 2, z: 3 }

// Rest operator (in function parameters)
const sumAll = (...args) => { // 'args' will be an array of all passed arguments
  return args.reduce((total, num) => total + num, 0);
};
console.log('Rest Operator Sum:', sumAll(1, 2, 3, 4, 5)); // Output: 15
```


#### 1.17 ES6 New Features

ES6 (ECMAScript 2015) introduced many significant features that revolutionized JavaScript development:

- let and const (block-scoped declarations)
- Arrow functions (=>)
- Template literals
- Destructuring assignment
- Spread syntax (...) and Rest parameters (...)
- Classes (syntactic sugar over prototypes)
- Default parameters for functions
- Modules (import/export)
- Promises
- for...of loop
- Map and Set data structures

Example (Arrow Functions):

```javascript
// Traditional function
const add = function(x, y) {
  return x + y;
};
console.log('Traditional function:', add(2, 3)); // Output: 5

// Arrow function (concise syntax for single expression)
const subtract = (x, y) => x - y;
console.log('Arrow function:', subtract(5, 2)); // Output: 3

// Arrow function with block body
const multiply = (x, y) => {
  const result = x * y;
  return result;
};
console.log('Arrow function with block:', multiply(4, 5)); // Output: 20
```


#### 1.18 async and defer attributes

The attributes async and defer are used in HTML <script> tags to control the loading and execution of external JavaScript files, impacting page rendering performance.

- **async**: When present, the script will be fetched asynchronously (in parallel with HTML parsing) and executed as soon as it is downloaded, potentially blocking HTML parsing if it finishes before parsing is complete. The order of execution for multiple async scripts is not guaranteed.
- **defer**: Also fetches the script asynchronously. However, scripts with defer will only be executed after the HTML document has been fully parsed and before the DOMContentLoaded event fires. Scripts with defer maintain their relative order of execution.

Example (HTML):

```html
<!DOCTYPE html>
<html>
<head>
  <title>Async vs Defer</title>
  <script async src="script-async.js"></script>
  <script defer src="script-defer-1.js"></script>
  <script defer src="script-defer-2.js"></script>
</head>
<body>
  <h1>Page Content</h1>
  <p>This is some content.</p>
  <script>
    console.log('Inline script executed'); // Executes after async/defer scripts are initiated, but before they run
  </script>
</body>
</html>
```

- script-async.js might execute before or after the inline script, depending on download time.
- script-defer-1.js will execute before script-defer-2.js, and both will execute after the HTML is parsed, but before DOMContentLoaded.


#### 1.19 Event Delegation and Event Propagation

- **Event Propagation**: Refers to the flow of events through the Document Object Model (DOM) tree. It has two phases:
    - Capturing Phase (downward): The event starts from the window object and travels down to the target element.
    - Bubbling Phase (upward): The event bubbles up from the target element back to the window object. Most event listeners default to the bubbling phase.
- **Event Delegation**: A design pattern where a single event listener is attached to a common parent element, instead of attaching individual listeners to multiple child elements. The listener then uses event bubbling to identify the actual target element that triggered the event. This is highly efficient for dynamic lists or large numbers of elements.

Example (Event Delegation):

```html
<ul id="myList">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>

<script>
  const myList = document.getElementById('myList');

  // Attach one listener to the parent <ul>
  myList.addEventListener('click', function(event) {
    // Check if the clicked element is an <li>
    if (event.target.tagName === 'LI') {
      console.log('Clicked on:', event.target.textContent);
      event.target.style.backgroundColor = 'yellow';
    }
  });

  // Dynamically add a new item
  const newItem = document.createElement('li');
  newItem.textContent = 'Item 4 (new)';
  myList.appendChild(newItem);
  // The new item will also be handled by the single listener due to delegation
</script>
```


#### 1.20 Debounce and Throttle

These are techniques used to control the frequency of function execution, especially for events that fire rapidly (e.g., scroll, resize, mousemove, input).

- **Debounce**: Delays the execution of a function until after a certain amount of time has passed since the last invocation. Useful for scenarios where you want to perform an action only after a user has stopped typing, resizing, etc., to avoid excessive calls (e.g., search suggestions, form validation).
- **Throttle**: Limits the rate at which a function can be called. It ensures that the function is executed at most once per specified time interval. Useful for scenarios like scroll events or continuous animations, where you want to ensure updates happen regularly but not too frequently to prevent performance issues.

Example (Conceptual - simplified):

```javascript
// Debounce function
function debounce(func, delay) {
  let timeout;
  return function(...args) {
    const context = this;
    clearTimeout(timeout);
    timeout = setTimeout(() => func.apply(context, args), delay);
  };
}

// Throttle function
function throttle(func, limit) {
  let inThrottle;
  return function(...args) {
    const context = this;
    if (!inThrottle) {
      func.apply(context, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// Example usage:
// document.getElementById('searchInput').addEventListener('input', debounce(function(e) {
//   console.log('Fetching search results for:', e.target.value);
// }, 500));

// window.addEventListener('scroll', throttle(function() {
//   console.log('Scroll event triggered!');
// }, 200));
```


#### 1.21 OOP in JavaScript (4 Pillars)

While JavaScript is primarily a prototype-based language, it supports object-oriented programming (OOP) concepts, especially with ES6 Classes (which are syntactic sugar over prototypes). The four pillars of OOP are:

- **Encapsulation**: Bundling data (properties) and methods that operate on the data within a single unit (e.g., an object or class), and restricting direct access to some of the object's components.
- **Inheritance**: A mechanism where one object (child/subclass) acquires the properties and behaviors of another object (parent/superclass). In JavaScript, this is achieved via the prototype chain or extends keyword with classes.
- **Polymorphism**: The ability of an object to take on many forms. In OOP, it allows objects of different classes to be treated as objects of a common type. This is often seen through method overriding or interfaces (conceptual in JS).
- **Abstraction**: Hiding the complex implementation details and showing only the essential features of an object. Users interact with a simplified interface without knowing the underlying complexity.

Example (Classes for OOP):

```javascript
// Encapsulation and Abstraction
class Animal {
  constructor(name) {
    this.name = name; // Public property
    let _sound = 'Generic sound'; // Private-like variable (closure)

    this.makeSound = function() { // Public method
      console.log(`${this.name} makes a ${_sound}.`);
    };

    this.setSound = function(newSound) { // Public method to modify private-like data
      _sound = newSound;
    };
  }
}

// Inheritance and Polymorphism
class Dog extends Animal { // Dog inherits from Animal
  constructor(name, breed) {
    super(name); // Call parent constructor
    this.breed = breed;
    this.setSound('Woof'); // Polymorphism: Dog overrides Animal's sound
  }

  fetch() {
    console.log(`${this.name} fetches the ball.`);
  }
}

const myDog = new Dog('Buddy', 'Golden Retriever');
myDog.makeSound(); // Output: Buddy makes a Woof. (Polymorphism in action)
myDog.fetch();     // Output: Buddy fetches the ball.

const genericAnimal = new Animal('Leo');
genericAnimal.makeSound(); // Output: Leo makes a Generic sound.
```


#### 1.22 Design Patterns in JavaScript

Design patterns are reusable solutions to common problems in software design. Some commonly used design patterns in JavaScript include:

- **Constructor Pattern**: Used for creating objects with shared properties and methods (e.g., using function Person(name) { this.name = name; }).
- **Factory Pattern**: An interface for creating objects, but lets subclasses decide which class to instantiate.
- **Module Pattern**: Used to encapsulate private and public methods/variables, creating a clean API for code. Often achieved with IIFEs (Immediately Invoked Function Expressions) or ES6 Modules.
- **Observer Pattern**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
- **Prototype Pattern**: Creates new objects by cloning an existing object (the prototype).
- **Singleton Pattern**: Ensures a class has only one instance and provides a global point of access to that instance.
- **Proxy Pattern**: Provides a placeholder or surrogate for another object to control access to it.

Example (Module Pattern - simplified):

```javascript
const ShoppingCart = (function() {
  let items = []; // Private variable
  function addItem(item) { // Private function
    items.push(item);
    console.log(`${item} added.`);
  }

  function removeItem(item) { // Private function
    items = items.filter(i => i !== item);
    console.log(`${item} removed.`);
  }

  return { // Public interface
    addToCart: function(item) {
      addItem(item);
    },
    viewCart: function() {
      console.log('Current cart:', items);
    },
    clearCart: function() {
      items = [];
      console.log('Cart cleared.');
    }
  };
})();

ShoppingCart.addToCart('Laptop');
ShoppingCart.addToCart('Mouse');
ShoppingCart.viewCart(); // Output: Current cart: ['Laptop', 'Mouse']
// ShoppingCart.addItem('Keyboard'); // Error: ShoppingCart.addItem is not a function (private)
```


#### 1.23 Deep Copy and Shallow Copy

These concepts are crucial when dealing with nested data structures (objects containing other objects or arrays) in JavaScript.

- **Shallow Copy**: Creates a new object but only copies references to the nested structures. This means that modifications made to the nested structures in the copied object will also affect the original object, and vice versa, because they both point to the same underlying nested objects.
    - Methods: Object.assign(), spread operator (...), Array.prototype.slice(), Array.from().
- **Deep Copy**: Creates a new object with its own values, completely independent of the original object, including all nested structures. Changes made to the copied object will not affect the original object, and vice versa.
    - Methods: JSON.parse(JSON.stringify(obj)) (simple cases), structured cloning algorithm (e.g., structuredClone() in modern browsers/Node.js), or custom recursive functions/libraries like Lodash's cloneDeep.

Example (Shallow Copy):

```javascript
// Original array with nested object
let arr1 = [10, 20, { nestedKey: 30 }, 40];

// Shallow copy using spread operator
let arr2 = [...arr1];

console.log('Original arr1 before modify:', arr1); // [10, 20, { nestedKey: 30 }, 40]
console.log('Shallow copy arr2 before modify:', arr2); // [10, 20, { nestedKey: 30 }, 40]

// Modify the nested object in arr2
arr2[^2].nestedKey = 11;

console.log('Original arr1 after modify:', arr1); // [10, 20, { nestedKey: 11 }, 40] - arr1 is affected!
console.log('Shallow copy arr2 after modify:', arr2); // [10, 20, { nestedKey: 11 }, 40]
```

Example (Deep Copy):

```javascript
// Original array of objects with nested values
let students = [
  { id: 1, name: 'abc', details: { age: 23 } },
  { id: 2, name: 'def', details: { age: 24 } },
  { id: 3, name: 'ghi', details: { age: 25 } }
];

// Deep copy using JSON.parse(JSON.stringify())
// NOTE: This method has limitations (e.g., loses functions, Dates, undefined, etc.)
let studentsCopy = JSON.parse(JSON.stringify(students));

console.log('Original students before modify:', students);
console.log('Deep copy studentsCopy before modify:', studentsCopy);

// Modify 'studentsCopy'
studentsCopy[^1].details.age = 30;

console.log('Original students after modify:', students); // students remains unaffected!
console.log('Deep copy studentsCopy after modify:', studentsCopy);
```


#### 1.24 Webpack Basics

Webpack is a powerful, open-source module bundler for JavaScript applications. Its main purpose is to bundle JavaScript files for usage in a browser, but it is also capable of transforming, bundling, or packaging nearly any resource or asset.

- **Module Bundler**: Takes various assets (JS, CSS, images, fonts) and bundles them into a few optimized files for the browser.
- **Loaders**: Transform different types of files into modules that can be consumed by Webpack's dependency graph (e.g., Babel loader for ES6+, CSS loader for CSS files).
- **Plugins**: Perform a wider range of tasks like optimization, asset management, and injection of environment variables.
- **Dependency Graph**: Webpack builds an internal graph of all dependencies in your project, starting from entry points.

Example (Conceptual webpack.config.js):

```javascript
// A simplified Webpack configuration file
const path = require('path');

module.exports = {
  mode: 'development', // or 'production'
  entry: './src/index.js', // The entry point of your application
  output: {
    filename: 'bundle.js', // The name of the output bundle
    path: path.resolve(__dirname, 'dist'), // The output directory
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Apply this rule to .js files
        exclude: /node_modules/, // Exclude node_modules
        use: {
          loader: 'babel-loader', // Use Babel to transpile JavaScript
          options: {
            presets: ['@babel/preset-env'],
          },
        },
      },
      {
        test: /\.css$/, // Apply this rule to .css files
        use: ['style-loader', 'css-loader'], // Use style-loader and css-loader
      },
    ],
  },
  devServer: {
    static: './dist', // Serve content from the 'dist' directory
  },
};
```


#### 1.25 Frequently Asked Questions for Frontend Developers (Selected Topics)

- **Pure and Impure Pipe/Function**:
    - **Pure Function**: A function that, given the same inputs, will always return the same output, and has no side effects (it doesn't modify any external state).
    - **Impure Function**: A function that may produce different outputs for the same inputs, or has side effects (modifies external state, performs I/O operations).
- **Mutability and Immutability**:
    - **Mutable**: An object whose state can be modified after it is created. (e.g., arrays, objects in JS by default).
    - **Immutable**: An object whose state cannot be modified after it is created. Any operation that appears to modify it actually returns a new object with the changes. (e.g., strings, numbers, booleans in JS; often achieved with libraries like Immer or Immutable.js for objects/arrays).
- **CORS (Cross-Origin Resource Sharing)**: A security mechanism implemented by web browsers that restricts web pages from making requests to a different domain than the one that served the web page. This prevents malicious scripts from making unauthorized requests to other sites.
- **Web Performance Optimization**: Techniques to improve the speed and responsiveness of web applications (e.g., minification, compression, lazy loading, image optimization, caching, critical CSS).
- **Responsive Web Design**: An approach to web design that makes web pages render well on a variety of devices and window or screen sizes (from minimal to wide desktop monitors). Achieved using flexible grids, layouts, images, and CSS media queries.
- **Microfrontend**: An architectural style where a large frontend application is decomposed into smaller, independently deployable frontend applications. Each microfrontend can be developed, deployed, and managed by a separate team.
- **PWA (Progressive Web App) and SPA (Single-Page Application)**:
    - **SPA**: A web application that loads a single HTML page and dynamically updates content as the user interacts with the app, without requiring full page reloads. Provides a desktop-like user experience.
    - **PWA**: A web application that uses modern web capabilities to deliver an app-like experience to users. They are reliable (offline support), fast, and engaging, leveraging technologies like Service Workers, Web App Manifests, and HTTPS.
- **Pre-processors - SCSS or LESS**: CSS pre-processors (like Sass/SCSS and Less) extend CSS with features like variables, nesting, mixins, functions, and inheritance, making CSS more maintainable and scalable. They compile down to regular CSS.
- **JWT (JSON Web Token)**: A compact, URL-safe means of representing claims to be transferred between two parties. Often used for authentication and authorization in web applications.
- **localStorage / sessionStorage**: Web Storage APIs for storing data in the browser.
    - **localStorage**: Stores data with no expiration date; data persists even after the browser is closed.
    - **sessionStorage**: Stores data for the duration of a single session; data is cleared when the browser tab is closed.
- **How to debug your frontend application**: Using browser developer tools (console, sources, network, elements tabs), setting breakpoints, logging messages, inspecting network requests, profiling performance.
- **Understand different use cases of the Promises with respect to API handling (retry API, combine 2-3 API)**:
    - **Retry API**: Implement a retry mechanism using Promises and setTimeout to re-attempt failed API calls a certain number of times.
    - **Combine 2-3 API**: Use Promise.all() to make multiple API calls concurrently and wait for all of them to resolve before proceeding, or Promise.race() to get the fastest response.


## 2. Angular

### Definition

Angular is a popular open-source, TypeScript-based front-end web application framework maintained by Google. It is used for building single-page applications (SPAs) and complex enterprise-level web applications. Angular provides a structured and opinionated way to develop web applications, emphasizing modularity, reusability, and maintainability.

### Key Concepts and Examples

#### 2.1 Angular Workflow

The Angular workflow describes the process of creating, building, and deploying Angular applications. It typically involves:

1. Setup: Installing Node.js, npm, and Angular CLI.
2. Project Creation: Using ng new to scaffold a new project.
3. Development: Creating components, services, modules, directives, pipes using ng generate. Writing logic in TypeScript, templates in HTML, and styling in CSS/SCSS.
4. Running: Using ng serve to run the development server with live reload.
5. Testing: Writing unit tests with Karma/Jasmine and end-to-end tests with Protractor/Cypress.
6. Building: Using ng build for production-ready optimized bundles (AOT compilation, tree shaking, minification).
7. Deployment: Deploying the dist folder content to a web server.

#### 2.2 Life Cycle Hooks in Angular

Angular components and directives have a lifecycle managed by Angular. Angular provides 8 life cycle hooks (methods) that you can implement to tap into key moments of this lifecycle:

- ngOnChanges: Called when Angular sets or resets data-bound input properties.
- ngOnInit: Called once, after the first ngOnChanges and after the component's inputs have been initialized. Good for initial data fetching.
- ngDoCheck: Called during every change detection cycle. Use with caution as it can impact performance if not optimized.
- ngAfterContentInit: Called once after Angular projects external content into the component's view.
- ngAfterContentChecked: Called after Angular checks the content projected into the directive or component.
- ngAfterViewInit: Called once after Angular initializes the component's views and child views.
- ngAfterViewChecked: Called after Angular checks the component's views and child views.
- ngOnDestroy: Called just before Angular destroys the component/directive. Good for unsubscribing from observables and detaching event handlers to prevent memory leaks.

Example:

```typescript
import { Component, OnInit, OnDestroy, OnChanges, SimpleChanges, Input } from '@angular/core';

@Component({
  selector: 'app-lifecycle-demo',
  template: `
    <p>Message: {{ message }}</p>
    <p>Input Value: {{ inputValue }}</p>
  `
})
export class LifecycleDemoComponent implements OnInit, OnDestroy, OnChanges {
  @Input() inputValue: string;
  message: string = 'Component initialized.';

  constructor() {
    console.log('Constructor called');
  }

  ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges called', changes);
    if (changes['inputValue']) {
      this.message = `Input changed to: ${this.inputValue}`;
    }
  }

  ngOnInit(): void {
    console.log('ngOnInit called');
    // Perform initial data loading here
  }

  ngDoCheck(): void {
    // console.log('ngDoCheck called'); // Be careful with this, it runs very frequently
  }

  ngOnDestroy(): void {
    console.log('ngOnDestroy called');
    // Clean up subscriptions, detach event listeners here
  }
}
```


#### 2.3 Component Communication in Angular

Sharing data between Angular components is essential for building interactive applications. Several methods exist:

- @Input() and @Output() properties: For parent-to-child (@Input()) and child-to-parent (@Output() with EventEmitter) communication.
- ViewChild and ContentChild decorators: To access a child component/directive/DOM element from a parent component's view (ViewChild) or projected content (ContentChild).
- Shared Services: For communication between unrelated components or for managing global state. Components inject the service and use its methods/properties.
- RxJS Subjects/Observables: For more complex, reactive communication patterns, especially with shared services.

Example (@Input() and @Output()):
**parent.component.ts**

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <h2>Parent Component</h2>
    <app-child [dataFromParent]="parentMessage" (childEvent)="handleChildEvent($event)"></app-child>
    <p>Message from Child: {{ messageFromChild }}</p>
    <button (click)="changeParentMessage()">Change Parent Message</button>
  `
})
export class ParentComponent {
  parentMessage: string = 'Hello from Parent!';
  messageFromChild: string = '';

  changeParentMessage() {
    this.parentMessage = 'Parent message updated!';
  }

  handleChildEvent(message: string) {
    this.messageFromChild = message;
    console.log('Parent received event from child:', message);
  }
}
```

**child.component.ts**

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `
    <h3>Child Component</h3>
    <p>Received from Parent: {{ dataFromParent }}</p>
    <button (click)="sendMessageToParent()">Send Message to Parent</button>
  `
})
export class ChildComponent {
  @Input() dataFromParent: string; // Input property to receive data
  @Output() childEvent = new EventEmitter<string>(); // Output property to emit events

  sendMessageToParent() {
    this.childEvent.emit('Hello from Child!'); // Emit an event with a message
  }
}
```


#### 2.4 Difference between ngIf and ngShow (AngularJS vs. Angular)

It's important to clarify that ngShow and ngHide were directives in AngularJS (the first version of Angular). In modern Angular (Angular 2+), the equivalent functionality is primarily handled by *ngIf and [hidden].

- **ngIf**: A structural directive that conditionally adds or removes an element (and its children) from the DOM based on a condition. When the condition is false, the element is completely removed from the DOM. This means listeners are detached, and components are destroyed.
- **[hidden] (or display: none via CSS)**: An attribute binding that conditionally shows or hides an element using CSS display property. The element remains in the DOM, but its visibility is toggled. Components are not destroyed, and listeners remain active.

Example (*ngIf and [hidden]):

```html
<button (click)="toggleVisibility()">Toggle Visibility</button>

<!-- Using *ngIf -->
<div *ngIf="isVisible" style="border: 1px solid green; padding: 10px;">
  This content is rendered with *ngIf. It is removed from DOM when hidden.
</div>

<!-- Using [hidden] -->
<div [hidden]="!isVisible" style="border: 1px solid blue; padding: 10px; margin-top: 10px;">
  This content is rendered with [hidden]. It remains in DOM but is hidden via CSS.
</div>
```

```typescript
// In your component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-conditional-display',
  templateUrl: './conditional-display.component.html'
})
export class ConditionalDisplayComponent {
  isVisible: boolean = true;

  toggleVisibility() {
    this.isVisible = !this.isVisible;
    console.log('Is visible:', this.isVisible);
  }
}
```


#### 2.5 Angular Pipes

Angular pipes are simple functions used for data transformation within templates. They allow developers to transform data before displaying it in the view, improving readability and reusability. Angular provides several built-in pipes (e.g., DatePipe, CurrencyPipe, UpperCasePipe, LowerCasePipe, DecimalPipe, JsonPipe), and you can also create custom pipes.

Example:

```html
<p>Original Date: {{ myDate }}</p>
<p>Formatted Date (short): {{ myDate | date:'short' }}</p>
<p>Formatted Date (medium): {{ myDate | date:'medium' }}</p>
<p>Currency (USD): {{ myAmount | currency:'USD':'symbol':'1.2-2' }}</p>
<p>Lowercase Text: {{ myText | lowercase }}</p>
<p>JSON Object: {{ myObject | json }}</p>
```

```typescript
// In your component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-pipe-demo',
  templateUrl: './pipe-demo.component.html'
})
export class PipeDemoComponent {
  myDate: Date = new Date();
  myAmount: number = 1234.5678;
  myText: string = 'Hello Angular Pipes!';
  myObject: any = { name: 'John', age: 30, city: 'Anytown' };
}
```


#### 2.6 Injectable and Singleton Services

- **@Injectable()**: A decorator that marks a class as available to the Dependency Injection (DI) system. It's typically used with services. When providedIn: 'root' is specified, the service becomes a singleton.
- **Singleton Services**: Services that are instantiated only once per application (when providedIn: 'root') and are shared across the entire application. This ensures that all components and other services that inject it receive the same instance, allowing for shared state and logic.

Example:

```typescript
// src/app/data.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root' // This makes DataService a singleton available throughout the app
})
export class DataService {
  private data: string[] = ['Item 1', 'Item 2'];

  constructor() {
    console.log('DataService instance created (should only happen once)');
  }

  getData(): string[] {
    return this.data;
  }

  addData(item: string) {
    this.data.push(item);
  }
}

// src/app/component-a/component-a.component.ts
import { Component } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-component-a',
  template: `
    <h3>Component A</h3>
    <p>Data: {{ dataService.getData() | json }}</p>
    <button (click)="dataService.addData('Item A')">Add Item A</button>
  `
})
export class ComponentAComponent {
  constructor(public dataService: DataService) {} // Inject the singleton service
}

// src/app/component-b/component-b.component.ts
import { Component } from '@angular/core';
import { DataService } from '../data.service';

@Component({
  selector: 'app-component-b',
  template: `
    <h3>Component B</h3>
    <p>Data: {{ dataService.getData() | json }}</p>
    <button (click)="dataService.addData('Item B')">Add Item B</button>
  `
})
export class ComponentBComponent {
  constructor(public dataService: DataService) {} // Inject the same singleton service
}
```


#### 2.7 Dependency Injection (DI) in Angular

Dependency Injection (DI) is a core design pattern in Angular. It's a way of supplying a new instance of a class with the fully formed dependencies it needs. Instead of a component creating its own dependencies, it receives them from an injector.

- **Benefits**: Improves testability, maintainability, and reusability by decoupling components from their dependencies.
- **Providers**: Tell the Angular injector how to create an instance of a service.
- **Injectors**: Responsible for creating and managing instances of dependencies.

Example:

```typescript
// src/app/logger.service.ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class LoggerService {
  log(message: string) {
    console.log(`[Logger]: ${message}`);
  }
}

// src/app/user.service.ts
import { Injectable } from '@angular/core';
import { LoggerService } from './logger.service';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  constructor(private logger: LoggerService) {} // Inject LoggerService

  getUsers() {
    this.logger.log('Fetching users...');
    // Simulate fetching users
    return [{ id: 1, name: 'Alice' }, { id: 2, name: 'Bob' }];
  }
}

// src/app/app.component.ts
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service'; // Import the service

@Component({
  selector: 'app-root',
  template: `
    <h1>User List</h1>
    <ul>
      <li *ngFor="let user of users">{{ user.name }}</li>
    </ul>
  `
})
export class AppComponent implements OnInit {
  users: any[];

  constructor(private userService: UserService) { // Angular injects UserService here
    console.log('AppComponent constructor');
  }

  ngOnInit() {
    this.users = this.userService.getUsers();
  }
}
```


#### 2.8 Host Listener and Host Binding

These are Angular decorators used to interact with the host element of a directive or component.

- **@HostListener()**: Used to listen to events on the host element (the element to which the directive or component is applied). When the specified event occurs, the decorated method is executed.
- **@HostBinding()**: Used to bind a property of the host element to a property of the directive or component. This allows you to dynamically set attributes, styles, or classes on the host element.

Example (Custom Highlight Directive):

```typescript
// src/app/highlight.directive.ts
import { Directive, ElementRef, HostListener, HostBinding, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]' // Apply as an attribute: <p appHighlight>
})
export class HighlightDirective {
  @Input('appHighlight') highlightColor: string; // Input property for custom color
  @HostBinding('style.backgroundColor') backgroundColor: string; // Bind to host element's background-color
  @HostBinding('class.highlighted') isHighlighted: boolean = false; // Bind to a CSS class

  constructor(private el: ElementRef) { }

  @HostListener('mouseenter') onMouseEnter() {
    this.backgroundColor = this.highlightColor || 'yellow'; // Set background on hover
    this.isHighlighted = true; // Add CSS class
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.backgroundColor = null; // Remove background on mouse leave
    this.isHighlighted = false; // Remove CSS class
  }

  @HostListener('click', ['$event.target']) onClick(targetElement) {
    console.log('Host element clicked:', targetElement);
  }
}
```

```html
<!-- In your app.component.html: -->
<p appHighlight="lightblue">Hover over me to highlight!</p>
<p appHighlight>Hover over me (default yellow)!</p>
```

```css
/* In your app.component.css (optional, for .highlighted class): */
.highlighted {
  font-weight: bold;
  border: 1px solid orange;
  padding: 5px;
}
```


#### 2.9 One-way and Two-way Data Binding

Data binding is the synchronization of data between the component's logic (TypeScript class) and its template (HTML view).

- **One-way Data Binding**: Data flows in a single direction.
    - From Component to View:
        - Interpolation ({{ }}): Displays component property values in the template.
        - Property Binding ([property]="value"): Binds a component property to a DOM element property or another component's input.
        - Attribute Binding ([attr.attribute]="value"): Binds a component property to an HTML attribute.
        - Class Binding ([class.className]="condition"): Adds/removes CSS classes based on a condition.
        - Style Binding ([style.property]="value"): Sets inline styles based on a property.
    - From View to Component:
        - Event Binding ((event)="handler()"): Listens for DOM events (e.g., click, input) and executes a component method.
- **Two-way Data Binding ([(ngModel)]="property")**: A combination of property binding and event binding, allowing data to flow in both directions. Changes in the component update the view, and changes in the view (e.g., user input in an <input>) update the component property. Requires FormsModule to be imported.

Example:

```html
<!-- One-way: Component to View (Interpolation & Property Binding) -->
<p>Hello, {{ userName }}!</p>
<img [src]="imageUrl" alt="Angular Logo" width="100">

<!-- One-way: View to Component (Event Binding) -->
<button (click)="incrementCount()">Click Me ({{ clickCount }})</button>

<!-- Two-way Data Binding -->
<input [(ngModel)]="twoWayMessage" placeholder="Type something...">
<p>You typed: {{ twoWayMessage }}</p>
```

```typescript
// In your component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-data-binding-demo',
  templateUrl: './data-binding-demo.component.html'
})
export class DataBindingDemoComponent {
  userName: string = 'Angular User';
  imageUrl: string = 'https://angular.io/assets/images/logos/angular/angular.svg';
  clickCount: number = 0;
  twoWayMessage: string = 'Initial message';

  incrementCount() {
    this.clickCount++;
  }
}
```


#### 2.10 Route/Auth Guards

Route guards in Angular are interfaces that you implement on classes to control navigation to, from, or between routes. They are essential for implementing authentication and authorization logic.

- **CanActivate**: Determines if a user can activate (navigate to) a route. Useful for authentication (e.g., ensuring a user is logged in).
- **CanActivateChild**: Determines if a user can activate a child route.
- **CanDeactivate**: Determines if a user can deactivate (leave) a route. Useful for preventing users from leaving a page with unsaved changes.
- **Resolve**: Pre-fetches data before a route is activated, ensuring the component has necessary data upon initialization.
- **CanLoad**: Determines if a module can be lazy-loaded. Useful for preventing unauthorized users from even downloading certain module code.

Example (CanActivate Auth Guard):

```typescript
// src/app/auth.guard.ts
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service'; // Assume you have an AuthService

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {

    if (this.authService.isLoggedIn()) { // Check if user is logged in
      return true; // Allow navigation
    } else {
      // Redirect to login page
      this.router.navigate(['/login']);
      return false; // Prevent navigation
    }
  }
}
```

```typescript
// In your app-routing.module.ts:
import { AuthGuard } from './auth.guard';
const routes: Routes = [
  { path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] },
  { path: 'login', component: LoginComponent },
  { path: '', redirectTo: '/dashboard', pathMatch: 'full' }
];
```


#### 2.11 Lazy Loading

Lazy loading is a technique in Angular where modules are loaded asynchronously, on-demand, rather than upfront when the application starts. This significantly improves the initial loading time of large applications by only loading the necessary modules when they are required, reducing the initial bundle size.

Example (Route Configuration for Lazy Loading):

```typescript
// src/app/app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  { path: 'home', component: HomeComponent }, // Eagerly loaded component
  {
    path: 'admin',
    // Lazy load the AdminModule when the 'admin' route is accessed
    loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule)
  },
  {
    path: 'products',
    // Lazy load the ProductsModule
    loadChildren: () => import('./products/products.module').then(m => m.ProductsModule)
  },
  { path: '**', component: NotFoundComponent } // Wildcard route for 404
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```


#### 2.12 Template/Reactive Forms and Validations

Angular provides two approaches for handling forms:

- **Template-driven Forms**: Rely heavily on directives in the template (ngModel, ngForm). They are simpler for basic forms but can become less manageable for complex scenarios. Angular infers the form model from the template.
- **Reactive Forms**: Use reactive programming with FormControl, FormGroup, and FormBuilder classes in the component's TypeScript code. They provide more control, are more scalable, and are easier to test. The form model is explicitly defined in the component.

Both approaches support validation.

- **Built-in Validators**: required, minlength, maxlength, pattern, email.
- **Custom Validators**: Functions that return a validation error object or null if valid.

Example (Reactive Form with Validation):

```typescript
// src/app/reactive-form-demo/reactive-form-demo.component.ts
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators, FormBuilder } from '@angular/forms';

@Component({
  selector: 'app-reactive-form-demo',
  templateUrl: './reactive-form-demo.component.html',
  styleUrls: ['./reactive-form-demo.component.css']
})
export class ReactiveFormDemoComponent implements OnInit {
  myForm: FormGroup;

  constructor(private fb: FormBuilder) {}

  ngOnInit(): void {
    this.myForm = this.fb.group({
      username: ['', [Validators.required, Validators.minLength(3)]],
      email: ['', [Validators.required, Validators.email]],
      password: ['', [Validators.required, Validators.minLength(6)]]
    });
  }

  onSubmit() {
    if (this.myForm.valid) {
      console.log('Form Submitted!', this.myForm.value);
      // Send data to backend
    } else {
      console.log('Form is invalid!');
      // Mark all fields as touched to display errors
      this.myForm.markAllAsTouched();
    }
  }

  // Helper to get form controls easily in template
  get f() { return this.myForm.controls; }
}
```

```html
<!-- reactive-form-demo.component.html -->
<form [formGroup]="myForm" (ngSubmit)="onSubmit()">
  <div>
    <label for="username">Username:</label>
    <input id="username" type="text" formControlName="username">
    <div *ngIf="f['username'].invalid && f['username'].touched" class="error">
      <div *ngIf="f['username'].errors?.['required']">Username is required.</div>
      <div *ngIf="f['username'].errors?.['minlength']">Username must be at least 3 characters.</div>
    </div>
  </div>

  <div>
    <label for="email">Email:</label>
    <input id="email" type="email" formControlName="email">
    <div *ngIf="f['email'].invalid && f['email'].touched" class="error">
      <div *ngIf="f['email'].errors?.['required']">Email is required.</div>
      <div *ngIf="f['email'].errors?.['email']">Invalid email format.</div>
    </div>
  </div>

  <div>
    <label for="password">Password:</label>
    <input id="password" type="password" formControlName="password">
    <div *ngIf="f['password'].invalid && f['password'].touched" class="error">
      <div *ngIf="f['password'].errors?.['required']">Password is required.</div>
      <div *ngIf="f['password'].errors?.['minlength']">Password must be at least 6 characters.</div>
    </div>
  </div>

  <button type="submit" [disabled]="myForm.invalid">Submit</button>
</form>
```

```css
/* reactive-form-demo.component.css */
.error {
  color: red;
  font-size: 0.8em;
  margin-top: 5px;
}
```


#### 2.13 Observable and Promises

Both are used for handling asynchronous operations, but they have key differences:

- **Promises**:
    - Represent a single future value or error.
    - Are "eager": they execute immediately upon creation.
    - Are not cancellable once initiated.
    - Do not support multiple values over time (only one resolve/reject).
- **Observables (from RxJS)**:
    - Represent a stream of values over time.
    - Are "lazy": they don't execute until something subscribes to them.
    - Are cancellable (by unsubscribing).
    - Can emit multiple values (like a stream), including zero, one, or many.
    - Provide powerful operators for transforming, combining, and manipulating streams.

When to use which:

- Promises: For single, one-time asynchronous operations (e.g., a single HTTP request).
- Observables: For continuous streams of data (e.g., real-time events, user input, multiple HTTP requests over time), or when you need advanced stream manipulation. Angular's HttpClient returns Observables.

Example (HTTP Request with Observable):

```typescript
// src/app/data.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

interface Post {
  id: number;
  title: string;
  body: string;
}

@Injectable({
  providedIn: 'root'
})
export class DataService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/posts';

  constructor(private http: HttpClient) { }

  getPosts(): Observable<Post[]> {
    return this.http.get<Post[]>(this.apiUrl);
  }
}
```

```typescript
// src/app/post-list/post-list.component.ts
import { Component, OnInit, OnDestroy } from '@angular/core';
import { DataService } from '../data.service';
import { Subscription } from 'rxjs'; // Import Subscription to manage subscriptions

@Component({
  selector: 'app-post-list',
  template: `
    <h2>Posts</h2>
    <div *ngIf="posts.length > 0">
      <div *ngFor="let post of posts" class="post-item">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </div>
    </div>
    <div *ngIf="posts.length === 0 && !errorMessage">Loading posts...</div>
    <div *ngIf="errorMessage" class="error-message">{{ errorMessage }}</div>
  `,
  styles: [`
    .post-item { border: 1px solid #eee; padding: 10px; margin-bottom: 10px; border-radius: 5px; }
    .error-message { color: red; }
  `]
})
export class PostListComponent implements OnInit, OnDestroy {
  posts: any[] = [];
  errorMessage: string = '';
  private postsSubscription: Subscription; // To store the subscription

  constructor(private dataService: DataService) { }

  ngOnInit(): void {
    this.postsSubscription = this.dataService.getPosts().subscribe({
      next: (data) => {
        this.posts = data;
        console.log('Posts loaded successfully:', data);
      },
      error: (err) => {
        this.errorMessage = 'Failed to load posts. Please try again later.';
        console.error('Error loading posts:', err);
      },
      complete: () => {
        console.log('Post fetching complete.');
      }
    });
  }

  ngOnDestroy(): void {
    // Unsubscribe to prevent memory leaks when the component is destroyed
    if (this.postsSubscription) {
      this.postsSubscription.unsubscribe();
    }
  }
}
```


#### 2.14 RxJS Operators in Angular

RxJS Operators are pure functions that enable functional programming style to handle collections of values with a declarative approach. They are used to manipulate, transform, and combine the data emitted by Observables.

- **Transformation Operators**: map, switchMap, mergeMap, concatMap, exhaustMap.
- **Filtering Operators**: filter, distinctUntilChanged, take, skip, takeUntil.
- **Combination Operators**: combineLatest, forkJoin.
- **Utility Operators**: tap, debounceTime, catchError.

Commonly Used RxJS Operators:

- **map**: Transforms each item emitted by an Observable into a new item.
- **switchMap**: Maps each value to an inner Observable, then flattens the Observables by unsubscribing from the previous inner Observable when a new one is emitted. Useful for "typeahead" searches where you only care about the latest request.
- **mergeMap (or flatMap)**: Maps each value to an inner Observable, then flattens the Observables by merging all values from all inner Observables. All inner Observables run in parallel.
- **concatMap**: Maps each value to an inner Observable, then flattens the Observables by concatenating them. It waits for the previous inner Observable to complete before subscribing to the next. Useful for sequential operations.
- **exhaustMap**: Maps each value to an inner Observable, then ignores all new incoming values while the inner Observable is still active. Useful for preventing multiple concurrent submissions (e.g., double-clicks on a submit button).
- **combineLatest**: Combines the latest values from multiple Observables and emits a new value whenever any of the input Observables emits.
- **distinctUntilChanged**: Emits a value from the source Observable only if it is different from the previous value emitted.
- **forkJoin**: Waits for all input Observables to complete and then emits an array of their last values. Similar to Promise.all().
- **debounceTime**: Waits for a specified duration to pass without any new emissions from the source Observable before emitting the latest value. Useful for search inputs.
- **catchError**: Catches errors on the source Observable and returns a new Observable or throws an error.
- **tap**: Performs a side effect for every emission on the source Observable, but returns an Observable that is identical to the source. Useful for debugging (e.g., console.log).
- **take**: Emits only the first n values emitted by the source Observable and then completes.
- **skip**: Skips the first n values emitted by the source Observable.
- **takeUntil**: Emits values from the source Observable until a notifier Observable emits a value. Useful for unsubscribing when a component is destroyed.

Example (switchMap for search):

```typescript
// src/app/search/search.component.ts
import { Component, OnInit, OnDestroy } from '@angular/core';
import { FormControl } from '@angular/forms';
import { DataService } from '../data.service'; // Assume DataService has a search method
import { debounceTime, distinctUntilChanged, switchMap, catchError } from 'rxjs/operators';
import { of, Subscription } from 'rxjs';

@Component({
  selector: 'app-search',
  template: `
    <input type="text" [formControl]="searchControl" placeholder="Search posts...">
    <div *ngIf="results.length > 0">
      <h3>Search Results:</h3>
      <ul>
        <li *ngFor="let result of results">{{ result.title }}</li>
      </ul>
    </div>
    <div *ngIf="isLoading">Loading...</div>
    <div *ngIf="error" class="error">{{ error }}</div>
  `,
  styles: [`
    .error { color: red; }
  `]
})
export class SearchComponent implements OnInit, OnDestroy {
  searchControl = new FormControl();
  results: any[] = [];
  isLoading: boolean = false;
  error: string = '';
  private searchSubscription: Subscription;

  constructor(private dataService: DataService) {}

  ngOnInit(): void {
    this.searchSubscription = this.searchControl.valueChanges.pipe(
      debounceTime(300), // Wait for 300ms after last keystroke
      distinctUntilChanged(), // Only emit if value is different from previous
      switchMap(searchTerm => { // Cancel previous search if new one starts
        this.isLoading = true;
        this.error = '';
        if (searchTerm.trim() === '') {
          this.isLoading = false;
          return of([]); // Return empty array if search term is empty
        }
        return this.dataService.searchPosts(searchTerm).pipe( // Assume dataService.searchPosts returns Observable<any[]>
          catchError(err => {
            this.error = 'Error during search.';
            this.isLoading = false;
            return of([]); // Return empty array on error
          })
        );
      })
    ).subscribe(data => {
      this.results = data;
      this.isLoading = false;
    });
  }

  ngOnDestroy(): void {
    if (this.searchSubscription) {
      this.searchSubscription.unsubscribe();
    }
  }
}
```


#### 2.15 Subject and Behavior Subject

These are special types of Observables from RxJS that act as both an Observable and an Observer. They can next() (emit values), error(), and complete(), and also be subscribed to.

- **Subject**: A multicast Observable. When an Observer subscribes to a Subject, it receives values emitted after the subscription. It does not hold any state.
- **BehaviorSubject**: A type of Subject that stores the "current" value. When an Observer subscribes to a BehaviorSubject, it immediately receives the last value emitted by the Subject (or its initial value) and then continues to receive all subsequent values. Useful for representing "state" that has an initial value.

Example:

```javascript
import { Subject, BehaviorSubject } from 'rxjs';

// Subject
const mySubject = new Subject<string>();

mySubject.subscribe(value => console.log('Subject Subscriber 1:', value)); // Subscribes now

mySubject.next('First value'); // Subscriber 1 receives 'First value'
mySubject.next('Second value'); // Subscriber 1 receives 'Second value'

mySubject.subscribe(value => console.log('Subject Subscriber 2:', value)); // Subscribes now

mySubject.next('Third value'); // Subscriber 1 & 2 receive 'Third value'

// BehaviorSubject
const myBehaviorSubject = new BehaviorSubject<string>('Initial Value'); // Needs an initial value

myBehaviorSubject.subscribe(value => console.log('BehaviorSubject Subscriber 1:', value)); // Receives 'Initial Value' immediately

myBehaviorSubject.next('New Value 1'); // Subscriber 1 receives 'New Value 1'

myBehaviorSubject.subscribe(value => console.log('BehaviorSubject Subscriber 2:', value)); // Receives 'New Value 1' immediately

myBehaviorSubject.next('New Value 2'); // Subscriber 1 & 2 receive 'New Value 2'
```


#### 2.16 HTTP (Req/Res) Interceptor

HTTP Interceptors in Angular are middleware that can intercept and handle HTTP requests and responses globally. They allow you to add common logic to all HTTP communications, such as:

- Adding authentication tokens to outgoing requests.
- Logging requests/responses.
- Error handling (e.g., redirecting to login on 401 Unauthorized).
- Modifying headers.
- Caching.

Interceptors are implemented as services that implement the HttpInterceptor interface.

Example (Auth Interceptor):

```typescript
// src/app/auth.interceptor.ts
import { Injectable } from '@angular/core';
import {
  HttpRequest,
  HttpHandler,
  HttpEvent,
  HttpInterceptor
} from '@angular/common/http';
import { Observable } from 'rxjs';
import { AuthService } from './auth.service'; // Assume AuthService provides a token

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  constructor(private authService: AuthService) {}

  intercept(request: HttpRequest<unknown>, next: HttpHandler): Observable<HttpEvent<unknown>> {
    const authToken = this.authService.getToken(); // Get token from service (e.g., localStorage)

    // Clone the request and add the authorization header
    if (authToken) {
      request = request.clone({
        setHeaders: {
          Authorization: `Bearer ${authToken}`
        }
      });
    }

    // Pass the cloned request to the next handler
    return next.handle(request);
  }
}
```

```typescript
// In your app.module.ts, provide the interceptor:
import { HTTP_INTERCEPTORS } from '@angular/common/http';
import { AuthInterceptor } from './auth.interceptor';

@NgModule({
  // ...
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptor,
      multi: true // multi: true is essential for providing multiple interceptors
    }
  ],
  // ...
})
export class AppModule { }
```


#### 2.17 Change Detection and OnPush Strategy

- **Change Detection**: The process by which Angular detects changes in component data and re-renders the view to reflect those changes. By default, Angular uses a heuristic approach: it checks every component from top to bottom whenever an asynchronous event occurs (e.g., HTTP request, setTimeout, user interaction).
- **OnPush Change Detection Strategy**: An optimization strategy that tells Angular to run change detection for a component (and its subtree) only when:

1. An @Input() property's reference changes (for objects/arrays, not just internal mutations).
2. An event originates from the component or one of its children.
3. An Observable that the component is subscribed to emits a new value.
4. Change detection is explicitly triggered (e.g., ChangeDetectorRef.detectChanges()).

Using OnPush can significantly improve performance in large applications by reducing the number of components Angular needs to check.

Example (OnPush):

```typescript
// src/app/on-push-demo/on-push-demo.component.ts
import { Component, Input, ChangeDetectionStrategy, ChangeDetectorRef } from '@angular/core';

@Component({
  selector: 'app-on-push-demo',
  template: `
    <h3>OnPush Component</h3>
    <p>Data: {{ data.value }}</p>
    <p>Random: {{ randomValue }}</p>
    <button (click)="updateInternal()">Update Internal Value</button>
    <button (click)="triggerChangeDetection()">Trigger CD Manually</button>
  `,
  changeDetection: ChangeDetectionStrategy.OnPush // Apply OnPush strategy
})
export class OnPushDemoComponent {
  @Input() data: { value: string }; // Input is an object
  randomValue: number = Math.random();

  constructor(private cdRef: ChangeDetectorRef) {}

  updateInternal() {
    this.randomValue = Math.random(); // This change won't trigger CD by itself
    console.log('Internal value updated, but UI might not reflect it unless input changes or CD is triggered.');
  }

  triggerChangeDetection() {
    this.cdRef.detectChanges(); // Manually trigger change detection
    console.log('Manually triggered change detection.');
  }
}
```

```typescript
// In parent component:
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent-on-push',
  template: `
    <h1>Parent Component (OnPush Demo)</h1>
    <app-on-push-demo [data]="parentData"></app-on-push-demo>
    <button (click)="changeParentData()">Change Parent Data (New Object Ref)</button>
    <button (click)="mutateParentData()">Mutate Parent Data (Same Object Ref)</button>
  `
})
export class ParentOnPushComponent {
  parentData = { value: 'Initial Parent Data' };

  changeParentData() {
    // This creates a NEW object reference, triggering OnPush CD
    this.parentData = { value: 'Updated Parent Data: ' + Math.random() };
    console.log('Parent data changed (new object reference).');
  }

  mutateParentData() {
    // This MUTATES the existing object, OnPush component won't detect this by default
    this.parentData.value = 'Mutated Parent Data: ' + Math.random();
    console.log('Parent data mutated (same object reference).');
  }
}
```


#### 2.18 Optimization Techniques in Angular

Optimizing Angular applications is crucial for performance and user experience.

1. Lazy Loading: Load modules and their associated components only when needed, reducing initial bundle size.
2. Tree Shaking: Eliminating unused code (dead code) from the final bundle during the build process.
3. Minification \& Uglification: Reducing file sizes by removing unnecessary characters (whitespace, comments) and shortening variable/function names.
4. OnPush Change Detection: Optimizing change detection cycles by only checking components when inputs change or events occur.
5. Optimized Asset Loading: Bundling, compression, using CDNs, and browser caching for images, fonts, and stylesheets.
6. Ahead-of-Time (AOT) Compilation: Compiling Angular HTML and TypeScript into efficient JavaScript during the build process (not in the browser), reducing runtime compilation overhead and improving startup performance.
7. Code Splitting: Breaking down the application code into smaller, asynchronously loaded chunks.
8. Service Worker and Progressive Web App (PWA) Support: Enabling offline capabilities, background syncing, and caching for an app-like experience.
9. Bundle Optimization: Further optimizing bundle size through advanced Webpack configurations (e.g., optimization.splitChunks).
10. Optimizing Angular Modules: Efficiently organizing modules, avoiding circular dependencies, and using lazy loading.
11. TrackBy function with *ngFor: Improves rendering performance for lists by helping Angular identify which items have changed, been added, or removed.
12. Detaching Change Detector: For highly dynamic parts, you can manually detach the change detector and reattach/mark for check only when necessary.

#### 2.19 dist and Bundle in Angular

- **dist (Distribution) Folder**: This is the output directory where the Angular CLI places the compiled, optimized, and bundled files of your application when you run ng build. This folder contains all the static assets (HTML, CSS, JavaScript, images) that are ready to be deployed to a web server.
- **Bundle**: Refers to the JavaScript files (and sometimes CSS) that Webpack (used internally by Angular CLI) generates by combining all your application's modules and their dependencies. These bundles are optimized for browser delivery, often minified, tree-shaken, and split into smaller chunks (e.g., main.js, polyfills.js, vendor.js, runtime.js, and lazy-loaded module chunks).


#### 2.20 Unit Testing in Angular

Unit testing in Angular involves testing individual units or components of an Angular application in isolation to ensure their functionality works as expected. Angular applications typically use:

- **Jasmine**: A behavior-driven development (BDD) framework for testing JavaScript code. It provides a clear and readable syntax for writing tests.
- **Karma**: A test runner that launches browsers and runs Jasmine tests against your code. It provides a testing environment.
- **Angular Testing Utilities**: Angular provides TestBed and other utilities to easily configure and create isolated testing environments for components, services, and directives.

Example (Component Unit Test):

```typescript
// src/app/counter/counter.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-counter',
  template: `
    <p>Count: {{ count }}</p>
    <button (click)="increment()">Increment</button>
    <button (click)="decrement()">Decrement</button>
  `
})
export class CounterComponent {
  count: number = 0;

  increment() {
    this.count++;
  }

  decrement() {
    this.count--;
  }
}
```

```typescript
// src/app/counter/counter.component.spec.ts
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { CounterComponent } from './counter.component';

describe('CounterComponent', () => {
  let component: CounterComponent;
  let fixture: ComponentFixture<CounterComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ CounterComponent ]
    })
    .compileComponents(); // Compile component's template and CSS
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(CounterComponent);
    component = fixture.componentInstance; // Get component instance
    fixture.detectChanges(); // Trigger initial change detection
  });

  it('should create the component', () => {
    expect(component).toBeTruthy();
  });

  it('should display initial count of 0', () => {
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('p').textContent).toContain('Count: 0');
  });

  it('should increment the count when increment button is clicked', () => {
    const incrementButton = fixture.nativeElement.querySelector('button:nth-child(1)');
    incrementButton.click();
    fixture.detectChanges(); // Trigger change detection after click
    expect(component.count).toBe(1);
    expect(fixture.nativeElement.querySelector('p').textContent).toContain('Count: 1');
  });

  it('should decrement the count when decrement button is clicked', () => {
    component.count = 5; // Set initial count for this test
    fixture.detectChanges();
    const decrementButton = fixture.nativeElement.querySelector('button:nth-child(2)');
    decrementButton.click();
    fixture.detectChanges();
    expect(component.count).toBe(4);
    expect(fixture.nativeElement.querySelector('p').textContent).toContain('Count: 4');
  });
});
```


#### 2.21 Shadow DOM

Shadow DOM is a web standard that allows for component-based styling and encapsulation. It enables developers to attach a hidden, separate DOM tree to an element, which is rendered along with the document's main DOM.

- **Encapsulation**: Styles and scripts defined within the Shadow DOM are isolated and do not leak out, nor do external styles leak in, preventing conflicts.
- **Reusability**: Promotes the creation of truly reusable web components with encapsulated behavior and styling.
- Angular uses Shadow DOM (or emulated Shadow DOM) for view encapsulation to achieve component style isolation.

Example (Conceptual HTML - Browser DevTools would show it):

```html
<!-- Main DOM -->
<my-custom-element>
  #shadow-root (open)
    <style>
      /* These styles only apply inside the shadow DOM */
      p { color: blue; }
    </style>
    <p>This is content inside the shadow DOM.</p>
</my-custom-element>
```


#### 2.22 Content Projection

Content projection (also known as transclusion in AngularJS) is a technique in Angular that allows you to insert or "project" content from a parent component into a designated placeholder within a child component's template. This makes components more flexible and reusable.

- Single-slot content projection: Uses <ng-content> without a select attribute. All projected content goes into this single slot.
- Multi-slot content projection: Uses <ng-content select="selector"> to project specific content based on a CSS selector (e.g., select="header", select="[footer]", select=".body").

Example:

```typescript
// card.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-card',
  template: `
    <div class="card">
      <div class="card-header">
        <ng-content select="[card-header]"></ng-content>
      </div>
      <div class="card-body">
        <ng-content></ng-content> <!-- Default slot for main content -->
      </div>
      <div class="card-footer">
        <ng-content select="[card-footer]"></ng-content>
      </div>
    </div>
  `,
  styles: [`
    .card { border: 1px solid #ddd; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); margin: 15px; overflow: hidden; }
    .card-header { background-color: #f0f0f0; padding: 10px; font-weight: bold; }
    .card-body { padding: 15px; }
    .card-footer { background-color: #f0f0f0; padding: 10px; font-size: 0.9em; text-align: right; }
  `]
})
export class CardComponent { }
```

```html
<!-- app.component.html (using the card component): -->
<app-card>
  <h2 card-header>My Awesome Card Title</h2>
  <p>This is the main content of the card. It can be any HTML.</p>
  <button card-footer>Action Button</button>
</app-card>

<app-card>
  <div card-header>
    <h3>Another Card</h3>
  </div>
  <p>More content here.</p>
  <small card-footer>Posted on July 5, 2025</small>
</app-card>
```


#### 2.23 View Encapsulation

View encapsulation is an Angular feature that controls how the component's styles are applied and isolated from the rest of the application. It prevents styles defined in one component from affecting other components and vice-versa.

- **ViewEncapsulation.Emulated (Default)**: Angular modifies the component's CSS selectors to make them unique, effectively scoping the styles to the component. This is achieved by adding unique attributes to component's DOM elements and corresponding attributes to CSS selectors.
- **ViewEncapsulation.ShadowDom**: Uses the browser's native Shadow DOM API to attach a Shadow DOM to the component's host element. Styles are truly encapsulated within this Shadow DOM.
- **ViewEncapsulation.None**: No view encapsulation is applied. Component styles become global and can affect other components, and global styles can affect the component. Use with caution.

Example:

```typescript
// src/app/encapsulation-demo/encapsulation-demo.component.ts
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-encapsulation-demo',
  template: `
    <div class="container">
      <h2>Encapsulation Demo</h2>
      <p>This paragraph has component-specific styling.</p>
    </div>
  `,
  styles: [`
    .container {
      border: 2px solid purple;
      padding: 15px;
      border-radius: 10px;
    }
    p {
      color: green;
      font-weight: bold;
    }
  `],
  // Change encapsulation strategy here:
  // encapsulation: ViewEncapsulation.Emulated // Default
  // encapsulation: ViewEncapsulation.ShadowDom
  // encapsulation: ViewEncapsulation.None
})
export class EncapsulationDemoComponent { }
```


#### 2.24 ::ng-deep and :host

These are special Angular pseudo-class selectors used for styling components, particularly when dealing with view encapsulation.

- **:host**: Selects the host element of the component itself (the custom HTML tag, e.g., <app-my-component>). Useful for applying styles directly to the component's root element.
- **::ng-deep (Deprecated, but still widely used)**: A "shadow-piercing" combinator that forces a style to pierce through view encapsulation and apply to child components, even if those children have their own encapsulation. It's generally discouraged due to its global impact and deprecation, favoring alternative approaches like ::part (for web components) or careful use of component inputs/outputs for styling.

Example:

```css
/* In component's CSS file (e.g., my-component.component.css) */

/* Styles the host element itself */
:host {
  display: block; /* Make the host element a block-level element */
  border: 1px solid blue;
  padding: 10px;
}

/* Styles a specific element inside the host */
:host h2 {
  color: navy;
}

/* Using ::ng-deep to style a child component's internal element (discouraged) */
/* This would style ALL 'p' tags inside any child component of this component */
/* ::ng-deep .some-child-component p {
  font-style: italic;
  color: gray;
} */
```


#### 2.25 Angular Signals (New Reactivity Model)

Angular Signals introduce a fine-grained reactivity system, allowing you to declare reactive values that automatically update the UI when changed. Signals provide a more predictable and efficient way to manage state and trigger change detection, reducing the need for manual subscriptions (especially for simple state management). They are a modern approach to reactivity, aiming to simplify state management and improve performance.

Example:

```typescript
import { Component, signal, computed, effect } from '@angular/core';

@Component({
  selector: 'app-signal-demo',
  template: `
    <h2>Signal Demo</h2>
    <p>Count: {{ count() }}</p>
    <p>Double Count: {{ doubleCount() }}</p>
    <button (click)="increment()">Increment</button>
    <button (click)="decrement()">Decrement</button>
  `
})
export class SignalDemoComponent {
  // Declare a writable signal
  count = signal(0);

  // Declare a computed signal (derived state)
  doubleCount = computed(() => this.count() * 2);

  constructor() {
    // An effect runs when its dependencies change
    effect(() => {
      console.log(`Current count is: ${this.count()}`);
    });
  }

  increment() {
    this.count.update(currentCount => currentCount + 1); // Update signal based on current value
    // Or: this.count.set(this.count() + 1);
  }

  decrement() {
    this.count.set(this.count() - 1); // Set signal to a new value
  }
}
```


#### 2.26 Standalone Components

Standalone Components allow you to create Angular components, directives, and pipes that are not tied to any NgModule. This simplifies the application structure, reduces boilerplate, and enables easier reuse and lazy loading. It's a significant step towards making Angular more modular and less dependent on the NgModule system.

Example:

```typescript
// src/app/standalone-button/standalone-button.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';
import { CommonModule } from '@angular/common'; // Import CommonModule for directives like ngIf, ngFor

@Component({
  selector: 'app-standalone-button',
  standalone: true, // Mark as standalone
  imports: [CommonModule], // Import necessary modules directly
  template: `
    <button (click)="onClick()" [style.background-color]="color" class="rounded-md px-4 py-2 text-white shadow-md">
      {{ label }}
    </button>
  `,
  styles: [`
    button {
      cursor: pointer;
      border: none;
      font-weight: bold;
      transition: background-color 0.3s ease;
    }
    button:hover {
      opacity: 0.9;
    }
  `]
})
export class StandaloneButtonComponent {
  @Input() label: string = 'Click Me';
  @Input() color: string = '#007bff';
  @Output() buttonClick = new EventEmitter<void>();

  onClick() {
    this.buttonClick.emit();
  }
}
```

```typescript
// In app.component.ts (or any other component/module that uses it):
import { Component } from '@angular/core';
import { StandaloneButtonComponent } from './standalone-button/standalone-button.component'; // Import directly

@Component({
  selector: 'app-root',
  standalone: true, // If app-root is also standalone
  imports: [StandaloneButtonComponent], // Import the standalone component
  template: `
    <h1>Standalone Components Demo</h1>
    <app-standalone-button label="Submit Form" color="green" (buttonClick)="handleSubmit()"></app-standalone-button>
    <app-standalone-button label="Cancel" color="red"></app-standalone-button>
  `
})
export class AppComponent {
  handleSubmit() {
    console.log('Form submitted!');
  }
}
```


#### 2.27 Angular Universal (Server-Side Rendering - SSR)

Angular Universal enables server-side rendering (SSR) for Angular applications. Instead of rendering the application solely in the browser, Angular Universal pre-renders the HTML on the server.

- **Benefits**:
    - Improved SEO: Search engine crawlers can easily index the content of your application, as they receive fully rendered HTML.
    - Faster Initial Load: Users see content immediately, improving perceived performance, especially on slow networks or devices, before the full JavaScript bundle loads and hydrates the application.
    - Better User Experience: Provides a more robust experience by serving static HTML first.


#### 2.28 Dynamic Component Loading

Dynamic Component Loading allows you to create and insert components into the DOM at runtime, rather than declaring them in the template during compilation. This is useful for:

- Building highly dynamic UIs (e.g., dashboards where widgets can be added/removed).
- Implementing plugin architectures.
- Creating modals, pop-ups, or notification messages.
- Lazy loading components that are not always needed.

Example (Conceptual):

```typescript
import { Component, ViewContainerRef, ComponentFactoryResolver, OnInit, OnDestroy } from '@angular/core';
// Assume you have a DynamicComponent to load
// import { DynamicComponent } from './dynamic.component';

@Component({
  selector: 'app-dynamic-loader',
  template: `
    <button (click)="loadComponent()">Load Dynamic Component</button>
    <div #dynamicComponentContainer></div> <!-- Placeholder for dynamic component -->
  `
})
export class DynamicLoaderComponent implements OnInit, OnDestroy {
  @ViewChild('dynamicComponentContainer', { read: ViewContainerRef, static: true })
  container: ViewContainerRef;

  constructor(private componentFactoryResolver: ComponentFactoryResolver) {}

  ngOnInit() {
    // For Angular 9+, you might use import() for lazy loading the component class
    // and then this.container.createComponent(componentClass);
  }

  async loadComponent() {
    // For older Angular versions (<9)
    // const componentFactory = this.componentFactoryResolver.resolveComponentFactory(DynamicComponent);
    // this.container.clear();
    // const componentRef = this.container.createComponent(componentFactory);
    // componentRef.instance.someInput = 'Data for dynamic component';

    // For Angular 9+ (Ivy) - simpler dynamic component creation
    const { DynamicComponent } = await import('./dynamic.component'); // Lazy load
    this.container.clear();
    const componentRef = this.container.createComponent(DynamicComponent);
    componentRef.instance.someInput = 'Data for dynamic component';
    componentRef.instance.someOutput.subscribe(event => {
      console.log('Dynamic component emitted:', event);
    });
  }

  ngOnDestroy() {
    // Clean up dynamically created components if necessary
    this.container.clear();
  }
}
```


#### 2.29 Angular Animations

Angular provides a robust API for creating complex UI transitions and effects, built on top of the Web Animations API. You can animate component entry/exit, state changes, and even route transitions, enhancing user experience and making applications feel more dynamic and responsive. Animations are defined using a declarative syntax in the component's metadata.

Example (Simple Fade In/Out Animation):

```typescript
import { Component, trigger, state, style, animate, transition } from '@angular/animations';

@Component({
  selector: 'app-fade-animation',
  template: `
    <button (click)="toggle()">Toggle Element</button>
    <div [@fade]="state" class="animated-box">
      I will fade in and out!
    </div>
  `,
  styles: [`
    .animated-box {
      width: 200px;
      height: 100px;
      background-color: lightblue;
      margin-top: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.2em;
    }
  `],
  animations: [
    trigger('fade', [
      state('void', style({ opacity: 0 })), // State when element is not in DOM
      transition('void <=> *', animate('500ms ease-in-out')) // Transition between void and any state
    ])
  ]
})
export class FadeAnimationComponent {
  state: 'void' | '*' = '*'; // Initial state for the animation

  toggle() {
    this.state = this.state === '*' ? 'void' : '*';
  }
}
```


#### 2.30 Internationalization (i18n)

Internationalization (i18n) in Angular helps you build applications that support multiple languages and regional formats using built-in tools and libraries. It covers:

- Translation of static content: Using i18n attributes in templates.
- Translation of dynamic content: Using \$localize or custom translation services.
- Formatting: Dates, numbers, currencies according to locale.
- Adapting layouts: For different text directions (RTL/LTR).

Angular CLI provides commands (ng extract-i18n) to extract translatable text into translation files (e.g., .xlf, .json).

#### 2.31 Angular Material/CDK

- **Angular Material**: A UI component library that implements Google's Material Design. It provides a rich set of pre-built, accessible, and responsive UI components (buttons, cards, forms, dialogs, etc.) that are consistent with Material Design guidelines.
- **Angular CDK (Component Dev Kit)**: A set of low-level, unstyled utilities and behaviors for building custom UI components. It provides common interaction patterns (e.g., drag-and-drop, overlays, accessibility helpers) without imposing any specific visual design. It's the foundation upon which Angular Material is built.

Using Material and CDK, you can quickly build visually appealing interfaces or create your own advanced UI features with the CDK's utilities.

#### 2.32 Custom Validators

Custom Validators allow you to implement your own validation logic for Angular forms, extending beyond the built-in validators (required, email, minlength, etc.). They are useful for enforcing specific business rules, validating complex input patterns, or performing asynchronous validation (e.g., checking if a username is available on the server).

- **Synchronous Validators**: Functions that return a ValidationErrors object (if invalid) or null (if valid).
- **Asynchronous Validators**: Functions that return a Promise<ValidationErrors | null> or Observable<ValidationErrors | null>.

Example (Custom Sync Validator for forbidden name):

```typescript
// src/app/shared/forbidden-name.validator.ts
import { AbstractControl, ValidatorFn, ValidationErrors } from '@angular/forms';

export function forbiddenNameValidator(nameRe: RegExp): ValidatorFn {
  return (control: AbstractControl): ValidationErrors | null => {
    const forbidden = nameRe.test(control.value);
    return forbidden ? { forbiddenName: { value: control.value } } : null;
  };
}
```

```typescript
// In your component (e.g., reactive-form-demo.component.ts):
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormControl, Validators, FormBuilder } from '@angular/forms';
import { forbiddenNameValidator } from '../shared/forbidden-name.validator'; // Import your custom validator

@Component({
  selector: 'app-reactive-form-demo',
  templateUrl: './reactive-form-demo.component.html'
})
export class ReactiveFormDemoComponent implements OnInit {
  myForm: FormGroup;

  constructor(private fb: FormBuilder) {}

  ngOnInit(): void {
    this.myForm = this.fb.group({
      username: ['', [
        Validators.required,
        Validators.minLength(3),
        forbiddenNameValidator(/admin|root/i) // Apply custom validator
      ]],
      email: ['', [Validators.required, Validators.email]]
    });
  }

  // ... rest of the component
}
```


#### 2.33 Dependency Injection Hierarchy

Dependency Injection Hierarchy describes how Angular provides and shares services at different levels of the application (root, module, component). This hierarchy affects the scope and lifetime of injected services.

- **providedIn: 'root'**: The service is provided at the root injector level, making it a singleton available throughout the entire application. This is the most common and recommended way for application-wide services.
- **providers array in @NgModule**: The service is provided at the module level. If the module is eagerly loaded, the service is a singleton within that module. If the module is lazy-loaded, a new instance of the service is created for that lazy-loaded module and its children.
- **providers array in @Component**: The service is provided at the component level. A new instance of the service is created for each instance of that component and its children. This creates a unique instance for each component.

Understanding this hierarchy is crucial for optimizing service usage, avoiding memory leaks, and controlling the visibility and lifetime of dependencies in large applications.

#### 2.34 Zone.js and NgZone

- **Zone.js**: A library that patches asynchronous browser APIs (like setTimeout, XMLHttpRequest, event listeners) to provide a "zone" of execution. It allows Angular to know when an asynchronous operation has completed, enabling it to trigger its change detection mechanism.
- **NgZone**: Angular's wrapper around Zone.js. It provides methods to run code inside or outside Angular's zone.
    - **run()**: Executes code within Angular's zone, ensuring change detection is triggered.
    - **runOutsideAngular()**: Executes code outside Angular's zone. This is useful for performance-critical operations (e.g., frequent third-party library calls, heavy computations) that don't need to trigger change detection on every tick, preventing unnecessary checks.

Example (Using NgZone.runOutsideAngular):

```typescript
import { Component, NgZone } from '@angular/core';

@Component({
  selector: 'app-zone-demo',
  template: `
    <p>Outside Angular Zone Updates: {{ outsideZoneCount }}</p>
    <p>Inside Angular Zone Updates: {{ insideZoneCount }}</p>
    <button (click)="startOutsideZone()">Start Outside Zone Updates</button>
    <button (click)="startInsideZone()">Start Inside Zone Updates</button>
  `
})
export class ZoneDemoComponent {
  outsideZoneCount: number = 0;
  insideZoneCount: number = 0;
  private intervalId: any;

  constructor(private ngZone: NgZone) {}

  startOutsideZone() {
    if (this.intervalId) clearInterval(this.intervalId);
    this.ngZone.runOutsideAngular(() => {
      this.intervalId = setInterval(() => {
        this.outsideZoneCount++;
        // UI will NOT update automatically here because we are outside Angular's zone
        // To update UI, we'd need to manually trigger change detection or run back inside the zone
        // this.ngZone.run(() => { this.insideZoneCount = this.outsideZoneCount; }); // Example of running back in
      }, 100);
    });
    console.log('Started updates outside Angular zone.');
  }

  startInsideZone() {
    if (this.intervalId) clearInterval(this.intervalId);
    this.intervalId = setInterval(() => {
      this.insideZoneCount++;
      // UI WILL update automatically here because we are inside Angular's zone
    }, 100);
    console.log('Started updates inside Angular zone.');
  }

  ngOnDestroy() {
    if (this.intervalId) clearInterval(this.intervalId);
  }
}
```


#### 2.35 State Management (NgRx, Akita, NGXS)

For large and complex Angular applications, managing application state can become challenging. State management libraries provide predictable and scalable ways to handle global and local state.

- **NgRx**: A reactive state management library inspired by Redux. It uses a single immutable state tree, pure functions (reducers), and Observables to manage state changes. It provides powerful tools for debugging (time-travel debugging) and enforcing unidirectional data flow.
- **Akita**: A state management pattern built on RxJS, designed to be simpler and less boilerplate-heavy than NgRx, while still leveraging Observables.
- **NGXS**: A state management pattern for Angular that uses a more declarative and class-based approach, aiming to reduce boilerplate compared to NgRx.

These libraries help make it easier to reason about and maintain your application's state, especially as it grows.

#### 2.36 ViewChild, ContentChild, ViewChildren, ContentChildren

These decorators let you access child components, directives, or DOM elements from a parent component.

- **@ViewChild()**: Used to query and get a reference to the first element or component matching the selector in the component's view template. Available after ngAfterViewInit.
- **@ViewChildren()**: Used to query and get references to all elements or components matching the selector in the component's view template. Returns a QueryList. Available after ngAfterViewInit.
- **@ContentChild()**: Used to query and get a reference to the first element or component matching the selector in the content projected into the component. Available after ngAfterContentInit.
- **@ContentChildren()**: Used to query and get references to all elements or components matching the selector in the content projected into the component. Returns a QueryList. Available after ngAfterContentInit.

Example (ViewChild):

```typescript
import { Component, ViewChild, ElementRef, AfterViewInit } from '@angular/core';

@Component({
  selector: 'app-child-access',
  template: `
    <input type="text" #myInput> <!-- Reference variable #myInput -->
    <button (click)="focusInput()">Focus Input</button>
  `
})
export class ChildAccessComponent implements AfterViewInit {
  @ViewChild('myInput') inputElement: ElementRef; // Get reference to the input element

  ngAfterViewInit(): void {
    console.log('Input element:', this.inputElement.nativeElement);
  }

  focusInput() {
    this.inputElement.nativeElement.focus();
    this.inputElement.nativeElement.value = 'Focused!';
  }
}
```


#### 2.37 Route Reuse Strategy

Route Reuse Strategy allows you to control when Angular reuses or destroys route components, enabling caching and improved navigation performance. By default, Angular destroys and recreates components when navigating between routes, even if the routes are similar. A custom strategy can be implemented to preserve component state, speed up navigation, and provide a smoother user experience (e.g., keeping a tab's state when switching tabs).

#### 2.38 Angular Security (XSS, CSRF, DomSanitizer)

Angular provides built-in mechanisms and best practices to protect your application from common web vulnerabilities:

- **XSS (Cross-Site Scripting)**: Angular automatically sanitizes values when binding them into the DOM, preventing malicious scripts from being injected.
- **CSRF (Cross-Site Request Forgery)**: Angular's HttpClient has built-in support for XSRF token validation (if configured on the backend).
- **DomSanitizer**: A service that helps you mark values as safe for use in the DOM when Angular's automatic sanitization would otherwise strip them (e.g., dynamic HTML, style URLs). Use with extreme caution and only when you are certain the content is safe.

It is important to sanitize user input, use Angular's security APIs, and follow secure coding practices to keep your application safe.

#### 2.39 Accessibility (a11y) in Angular

Accessibility (a11y) ensures your Angular application is usable by everyone, including people with disabilities. Building accessible apps is not only a legal requirement in many regions but also improves usability for all users. Angular, especially with Angular Material/CDK, provides tools and guidance for building accessible applications:

- ARIA attributes: Using aria-* attributes to provide semantic information for assistive technologies.
- Keyboard navigation: Ensuring all interactive elements are navigable and operable via keyboard.
- Semantic HTML: Using appropriate HTML elements (<button>, <input>, <nav>, etc.) for their intended purpose.
- Focus management: Managing focus programmatically for dynamic content changes (e.g., modals).
- Contrast ratios: Ensuring sufficient color contrast for readability.
- Alternative text: Providing alt text for images.

<div style="text-align: center">⁂</div>

[^1]: Angular-and-JavaScript.txt

