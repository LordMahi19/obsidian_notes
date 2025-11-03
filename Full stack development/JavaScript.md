# JavaScript DOM Manipulation

This page contains notes related to interacting with the Document Object Model (DOM) using JavaScript.

## What is the DOM?

The DOM is a programming interface for web documents. It represents the page so that programs can change the document structure, style, and content. The DOM represents the document as a tree of objects; each node in the tree represents a part of the document (e.g., an element, text, or attribute).

---

## Selecting Elements (Queries)

- `document.getElementById('id')` — Selects a single element by its unique `id`. Returns the element or `null`.
- `document.getElementsByTagName('tag')` — Selects all elements with the given tag name. Returns a live `HTMLCollection`.
- `document.getElementsByClassName('class')` — Selects all elements with the given class name. Returns a live `HTMLCollection`.
- `document.querySelector('selector')` — Selects the **first** element that matches a CSS selector. Returns the element or `null`.
- `document.querySelectorAll('selector')` — Selects **all** elements that match a CSS selector. Returns a static `NodeList`.

**`HTMLCollection` vs. `NodeList`:**
- `HTMLCollection`: Live collection. It automatically updates if elements are added or removed from the DOM.
- `NodeList`: Static collection (usually). It's a snapshot of the elements at the time of the query. `querySelectorAll` returns a static one.

---

## Traversing the DOM

Once you have an element, you can navigate to its relatives.

**Parent:**
- `element.parentElement` — The parent element.
- `element.parentNode` — The parent node (can be an element, document, or document fragment).

**Children:**
- `element.children` — `HTMLCollection` of child elements.
- `element.childNodes` — `NodeList` of all child nodes (including text and comment nodes).
- `element.firstElementChild` / `element.lastElementChild` — First/last child element.
- `element.firstChild` / `element.lastChild` — First/last child node.

**Siblings:**
- `element.previousElementSibling` / `element.nextElementSibling` — Previous/next sibling element.
- `element.previousSibling` / `element.nextSibling` — Previous/next sibling node.

---

## Manipulating Elements

**Content:**
- `element.innerHTML` — Gets or sets the HTML content inside an element. **Warning:** Setting it can be a security risk (XSS) if the content is from a user.
- `element.textContent` — Gets or sets the text content (no HTML). Faster and safer than `innerHTML`.
- `element.innerText` — Similar to `textContent`, but is aware of rendered appearance (e.g., doesn't include hidden text). Can be slower.

**Attributes:**
- `element.getAttribute('attr')` / `element.setAttribute('attr', 'value')`
- `element.hasAttribute('attr')` / `element.removeAttribute('attr')`
- Direct access for standard attributes: `element.id`, `element.href`, `element.src`.

**Classes:**
- `element.className` — Gets or sets the entire `class` attribute string.
- `element.classList` — A more convenient API for managing classes:
    - `element.classList.add('class')`
    - `element.classList.remove('class')`
    - `element.classList.toggle('class')`
    - `element.classList.contains('class')`
    - `element.classList.replace('old', 'new')`

**Styles:**
- `element.style.property` — Gets or sets inline styles. Property names are camelCased (e.g., `backgroundColor`).
- `window.getComputedStyle(element)` — Gets the final, computed styles for an element (readonly).

---

## Creating & Inserting Elements

1.  **Create:** `const newEl = document.createElement('div');`
2.  **Modify:** `newEl.textContent = 'Hello!';`
3.  **Insert:**
    - `parentElement.appendChild(newEl)` — Adds `newEl` as the last child of `parentElement`.
    - `parentElement.prepend(newEl)` — Adds `newEl` as the first child.
    - `referenceElement.before(newEl)` — Inserts `newEl` before `referenceElement`.
    - `referenceElement.after(newEl)` — Inserts `newEl` after `referenceElement`.
    - `referenceElement.replaceWith(newEl)` — Replaces `referenceElement` with `newEl`.

**Removing Elements:**
- `childElement.remove()` — Removes the element from the DOM.
- `parentElement.removeChild(childElement)` — The older way.

---

## Events

Events are actions that happen in the browser, like a user clicking a button or a page finishing loading.

**Adding Event Listeners:**
- `element.addEventListener('event-type', callbackFunction)`
- `element.addEventListener('click', (event) => { ... });`

**Common Event Types:**
- **Mouse:** `click`, `dblclick`, `mousedown`, `mouseup`, `mouseover`, `mouseout`, `mousemove`, `contextmenu`.
- **Keyboard:** `keydown`, `keyup`, `keypress`.
- **Form:** `submit`, `change` (for inputs, selects), `input`, `focus`, `blur`.
- **Window/Document:** `load`, `DOMContentLoaded`, `resize`, `scroll`.

**The `event` Object:**
The callback function receives an `event` object with useful properties:
- `event.target` — The element that triggered the event.
- `event.currentTarget` — The element the listener is attached to.
- `event.preventDefault()` — Stops the browser's default behavior (e.g., form submission).
- `event.stopPropagation()` — Stops the event from bubbling up to parent elements.
- `event.key` (for keyboard events).
- `event.clientX` / `event.clientY` (for mouse events).

**Removing Event Listeners:**
- `element.removeEventListener('event-type', callbackFunction)`
- **Important:** You must pass the *exact same function reference* that was used for `addEventListener`. Anonymous functions won't work.

---

## Document & Window

- `document` — Represents the entire page. Entry point to the DOM.
- `window` — Represents the browser window/tab. Global object in browser JS.
    - `window.innerWidth` / `window.innerHeight`
    - `window.location` (URL info)
    - `window.localStorage` / `window.sessionStorage`
    - `window.alert()`, `window.prompt()`, `window.confirm()`
    - `window.setTimeout()`, `window.setInterval()`

# Core JavaScript Language

This section covers the fundamental concepts of the JavaScript language itself.

---

## Variables & Data Types

**Declaration:**
- `var`: Function-scoped. Can be re-declared and updated. Hoisted. (Legacy)
- `let`: Block-scoped (`{}`). Can be updated but not re-declared in the same scope. Hoisted but in a "temporal dead zone".
- `const`: Block-scoped. Cannot be updated or re-declared. The value itself can be mutable if it's an object or array.

**Primitive Types:**
- `string`: Text.
- `number`: Integers and floating-point numbers. Includes `Infinity`, `-Infinity`, and `NaN`.
- `boolean`: `true` or `false`.
- `null`: Intentional absence of any object value.
- `undefined`: A variable that has been declared but not assigned a value.
- `symbol`: A unique and immutable primitive value.
- `bigint`: For integers of arbitrary precision.

**Type Coercion:**
JavaScript is loosely typed and will often automatically convert types.
- `==` (Loose Equality): Performs type coercion. `5 == '5'` is `true`.
- `===` (Strict Equality): Does not perform type coercion. `5 === '5'` is `false`. (Generally preferred)

---

## Operators

- **Arithmetic:** `+`, `-`, `*`, `/`, `%` (modulus), `**` (exponentiation), `++` (increment), `--` (decrement).
- **Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, `%=`.
- **Comparison:** `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=`.
- **Logical:** `&&` (AND), `||` (OR), `!` (NOT).
- **Ternary:** `condition ? exprIfTrue : exprIfFalse`.
- **Typeof:** `typeof myVar` — Returns a string indicating the type.

---

## Control Flow

**Conditional:**
- `if (condition) { ... } else if (condition) { ... } else { ... }`
- `switch (expression) { case value: ...; break; default: ...; }`

**Loops:**
- `for (let i = 0; i < 5; i++) { ... }` — Standard loop.
- `while (condition) { ... }` — Loops while condition is true.
- `do { ... } while (condition)` — Executes once, then loops while condition is true.
- `for...of` — Iterates over iterable objects (like arrays, strings). `for (const item of myArray) { ... }`
- `for...in` — Iterates over the properties of an object. `for (const key in myObject) { ... }`

---

## Functions

**Declaration:**
'''javascript
function add(a, b) {
  return a + b;
}
'''

**Expression:**
'''javascript
const add = function(a, b) {
  return a + b;
};
'''

**Arrow Functions (ES6):**
- Concise syntax.
- Do not have their own `this`, `arguments`, `super`, or `new.target`. They inherit `this` from the parent scope.
'''javascript
const add = (a, b) => a + b;

const greet = name => `Hello, ${name}!`;

const doSomething = () => {
  // multi-line
  return 'done';
};
'''

**Parameters:**
- **Default Parameters:** `function greet(name = 'Guest') { ... }`
- **Rest Parameters:** `function sum(...numbers) { ... }` (collects all arguments into an array)

---

## Objects

A collection of key-value pairs.

**Literal:**
'''javascript
const person = {
  firstName: 'John',
  lastName: 'Doe',
  age: 30,
  greet: function() {
    return `Hello, ${this.firstName}`;
  }
};
'''

**Accessing Properties:**
- Dot Notation: `person.firstName`
- Bracket Notation: `person['lastName']` (useful for dynamic keys)

**`this` Keyword:**
The value of `this` depends on how a function is called.
- In an object method: `this` refers to the object.
- In a regular function: `this` is the global object (`window` in browsers) in non-strict mode, or `undefined` in strict mode.
- In an arrow function: `this` is inherited from the enclosing scope.

---

## Arrays

Ordered lists of values.

**Literal:**
`const fruits = ['apple', 'banana', 'cherry'];`

**Common Methods:**
- `array.length` — Get size.
- `array.push(item)` / `array.pop()` — Add/remove from end.
- `array.unshift(item)` / `array.shift()` — Add/remove from start.
- `array.indexOf(item)` — Find index of an item.
- `array.slice(start, end)` — Returns a shallow copy of a portion of an array.
- `array.splice(start, deleteCount, item1, ...)` — Changes the contents of an array by removing or replacing existing elements and/or adding new ones in place.

**Iteration Methods:**
- `array.forEach(item => { ... })` — Executes a function for each element.
- `array.map(item => { ... })` — Creates a new array with the results of calling a function for every array element.
- `array.filter(item => { ... })` — Creates a new array with all elements that pass the test implemented by the provided function.
- `array.reduce((accumulator, item) => { ... }, initialValue)` — Reduces the array to a single value.
- `array.find(item => { ... })` — Returns the first element that satisfies the condition.
- `array.some(item => { ... })` — Checks if at least one element passes the test.
- `array.every(item => { ... })` — Checks if all elements pass the test.

---

## ES6+ Features

**Destructuring:**
- **Object:** `const { firstName, age } = person;`
- **Array:** `const [first, second] = fruits;`

**Spread & Rest Syntax (`...`):**
- **Spread:** Expands an iterable (like an array or object) into individual elements.
  `const newArray = [...oldArray, 'a', 'b'];`
  `const newObject = { ...oldObject, newProp: 'value' };`
- **Rest:** Collects multiple elements into a single array (see Functions section).

**Template Literals:**
- Backticks (`` ` ``) for strings.
- Allows embedded expressions: `` `Hello, ${name}!` ``
- Allows multi-line strings.

**Classes:**
- Syntactic sugar over JavaScript's prototype-based inheritance.
'''javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, ${this.name}`;
  }
}

class Student extends Person {
  constructor(name, major) {
    super(name); // call parent constructor
    this.major = major;
  }
}
'''

**Modules (ESM):**
- **Export:** `export const myVar = 5;` or `export default myFunction;`
- **Import:** `import { myVar } from './file.js';` or `import myFunc from './file.js';`

---

## Asynchronous JavaScript

**Callbacks:**
- A function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.
- Can lead to "callback hell" (nested callbacks).

**Promises:**
- An object representing the eventual completion (or failure) of an asynchronous operation.
- States: `pending`, `fulfilled`, `rejected`.
- `.then(onFulfilled, onRejected)`: Handles the result.
- `.catch(onRejected)`: Handles errors.
- `.finally(() => { ... })`: Executes regardless of outcome.

'''javascript
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
'''

**Async/Await:**
- Syntactic sugar on top of Promises, making async code look more synchronous.
- `async` keyword makes a function return a Promise.
- `await` keyword pauses the function execution until a Promise is settled. Must be used inside an `async` function.

'''javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}
'''