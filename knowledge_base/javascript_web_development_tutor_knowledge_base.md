# JavaScript Knowledge Base for Web Development Tutor RAG Chatbot

## 1. What JavaScript is and how it differs from HTML and CSS

### Definition
JavaScript is a high-level, interpreted programming language that conforms to the ECMAScript specification. It is a core technology of the World Wide Web, enabling interactive web pages and dynamic behavior.

### Difference from HTML and CSS
* **HTML (HyperText Markup Language):** The skeleton/structure of a webpage. It defines elements like headings, paragraphs, links, and images.
* **CSS (Cascading Style Sheets):** The presentation/skin of a webpage. It controls visual styling, layouts, colors, and fonts.
* **JavaScript (JS):** The behavior/brain of a webpage. It handles logic, user interactions, data processing, communication with servers, and dynamic DOM manipulation.

### Syntax & Example
```javascript
// JavaScript logic to change text content
document.getElementById("title").innerText = "Hello, JavaScript!";
```

### Output / Behavior
Finds an HTML element with the `id="title"` and updates its text content dynamically on the webpage.

### Explanation
While HTML provides static content and CSS makes it look appealing, JavaScript executes instructions to modify content, respond to clicks, fetch data from servers, and perform computations.

### Common Mistakes
* Treating JavaScript as a styling or layout language.
* Confusing HTML tags with JavaScript functions.

### Best Practices
* Keep concerns separated: use HTML for structure, CSS for style, and JavaScript strictly for behavior.
* Always load JavaScript asynchronously or defer its execution unless it's required immediately in the `<head>`.

---

## 2. Running JavaScript in browsers, script tags, external files, and browser developer tools

### Definition
JavaScript code can be executed directly inside web browsers using inline script tags, external script files linked via HTML, or interactively within the browser Developer Tools console.

### Syntax
```html
<!-- External Script Tag -->
<script src="script.js" defer></script>

<!-- Inline Script Tag -->
<script>
  console.log("Running inline JavaScript");
</script>
```

### Output / Behavior
Outputs `"Running inline JavaScript"` to the browser's developer tools console when the webpage loads.

### Explanation
Modern browsers have built-in JavaScript engines (like Google Chrome's V8) that parse and execute JS code. Using external `.js` files keeps code organized, cacheable, and maintainable.

### Common Mistakes
* Placing `<script>` tags at the very top of the `<body>` without `defer` or `async`, which can block HTML parsing.
* Forgetting to link the external script file properly.

### Best Practices
* Use external `.js` files for all production web applications.
* Use the `defer` attribute on script tags in the `<head>` so they execute after the HTML document is fully parsed.

---

## 3. Variables: let, const, and var; naming rules and scope

### Definition
Variables are containers for storing data values. In modern JavaScript, we use `let` and `const` (introduced in ES6), avoiding legacy `var`.
* `const`: Cannot be reassigned.
* `let`: Can be reassigned.
* `var`: Function-scoped, prone to hoisting bugs.

### Syntax
```javascript
const appName = "WebDevTutor"; // Cannot be reassigned
let userScore = 0;              // Can be reassigned
var legacyVar = "avoid this";   // Function-scoped
```

### Output / Behavior
```javascript
userScore = 10; // Valid
// appName = "NewApp"; -> TypeError: Assignment to constant variable.
```

### Explanation
`let` and `const` are block-scoped (scoped to the nearest `{ }`). Naming rules require identifiers to start with a letter, underscore (`_`), or dollar sign (`$`), and cannot use reserved keywords.

### Common Mistakes
* Using `const` on primitive variables that genuinely need to change later.
* Relying on `var` and running into unexpected variable hoisting bugs.

### Best Practices
* Default to `const` for everything. Use `let` only when you know the variable's value will need to be reassigned. Never use `var`.
* Use camelCase for variable names (e.g., `userScore`, `isActive`).

---

## 4. Data types, primitive values, objects, typeof, and type conversion

### Definition
JavaScript has primitive data types (immutable values) and reference types (objects).
* **Primitives:** `string`, `number`, `boolean`, `undefined`, `null`, `symbol`, `bigint`.
* **Objects:** Collections of key-value pairs (including arrays and functions).

### Syntax
```javascript
const name = "Alice";      // string
const age = 25;            // number
const isOnline = true;     // boolean
const user = { name: "Bob" }; // object

console.log(typeof age);   // "number"
const converted = String(age); // Explicit conversion
```

### Output / Behavior
```text
number
```

### Explanation
`typeof` is an operator used to check the data type of a variable. Type conversion can be explicit (`String()`, `Number()`, `Boolean()`) or implicit (coercion performed automatically by JavaScript).

### Common Mistakes
* Assuming `typeof null` returns `"null"` (it actually returns `"object"` due to a historical bug).
* Accidentally concatenating strings and numbers during implicit coercion (e.g., `"5" + 5` results in `"55"`).

### Best Practices
* Perform explicit type conversion when working with user input or API parameters to avoid coercion bugs.
* Use strict equality operators (`===`) to prevent unexpected type coercion.

---

## 5. Operators, comparisons, logical operators, truthy and falsy values, and short-circuiting

### Definition
Operators perform operations on values. Comparisons evaluate relationships. Logical operators (`&&`, `||`, `!`) combine expressions. Falsy values include `false`, `0`, `""`, `null`, `undefined`, and `NaN`. Everything else is truthy.

### Syntax
```javascript
const x = 10;
const y = 20;

const isGreater = x > y; // false
const result = x && "Hello"; // "Hello" (short-circuit)
const fallback = null || "Default"; // "Default"
```

### Output / Behavior
Evaluates logical expressions using short-circuit evaluation (stopping as soon as the outcome is determined).

### Explanation
Logical `&&` returns the first falsy operand or the last truthy operand. Logical `||` returns the first truthy operand or the last falsy operand.

### Common Mistakes
* Confusing loose equality (`==`) with strict equality (`===`).
* Forgetting that empty arrays `[]` and empty objects `{}` are truthy in JavaScript.

### Best Practices
* Always use strict equality (`===` and `!==`).
* Leverage short-circuit evaluation (`||`) for clean default values.

---

## 6. Strings, template literals, string methods, and formatting

### Definition
Strings represent textual data. Template literals (using backticks `` ` ``) allow string interpolation and multiline strings.

### Syntax
```javascript
const firstName = "Jane";
const greeting = `Hello, ${firstName}! Welcome to JS.`;

console.log(greeting.length);
console.log(greeting.toUpperCase());
console.log(greeting.includes("Welcome"));
```

### Output / Behavior
```text
Hello, Jane! Welcome to JS.
29
HELLO, JANE! WELCOME TO JS.
true
```

### Explanation
String methods like `.slice()`, `.split()`, `.replace()`, and `.trim()` allow powerful text manipulation without modifying the original string (since primitives are immutable).

### Common Mistakes
* Using regular quotes (`'` or `"`) when string interpolation with variables is needed.
* Forgetting that string indices are 0-based.

### Best Practices
* Prefer template literals over string concatenation (`+`) for better readability.
* Always use built-in string methods instead of writing custom parsing loops when possible.

---

## 7. Numbers, mathematical operations, Math, and random numbers

### Definition
JavaScript has only one number type: double-precision 64-bit floating point. The `Math` object provides mathematical constants and functions.

### Syntax
```javascript
const sum = 5 + 3 * 2; // 11 (operator precedence)
const rounded = Math.round(4.7); // 5
const randomNum = Math.floor(Math.random() * 10) + 1; // 1 to 10
```

### Output / Behavior
Generates pseudo-random integers between 1 and 10.

### Explanation
Floating-point arithmetic can lead to precision quirks (e.g., `0.1 + 0.2 !== 0.3`). The `Math` object contains helpful methods like `Math.max()`, `Math.min()`, `Math.floor()`, and `Math.ceil()`.

### Common Mistakes
* Relying on exact floating-point equality comparisons for decimals.
* Misunderstanding `Math.random()` (which returns a number from 0 up to, but not including, 1).

### Best Practices
* Use `.toFixed()` when displaying decimals to users (keeping in mind it returns a string).
* Use `Number.isInteger()` to safely check if a number is an integer.

---

## 8. Conditional statements: if, else, else if, switch, and ternary expressions

### Definition
Conditional statements execute different blocks of code based on whether specified conditions evaluate to truthy or falsy.

### Syntax
```javascript
const role = "admin";

// If/Else
if (role === "admin") {
  console.log("Welcome Admin");
} else {
  console.log("Welcome User");
}

// Ternary Operator
const access = role === "admin" ? "Full Access" : "Limited Access";

// Switch
switch (role) {
  case "admin":
    console.log("Admin panel");
    break;
  default:
    console.log("Home page");
}
```

### Output / Behavior
Evaluates variables and executes corresponding code branches.

### Explanation
Ternary expressions (`condition ? trueExpr : falseExpr`) are concise shortcuts for simple `if/else` statements. `switch` statements are useful for checking a single expression against multiple fixed values.

### Common Mistakes
* Forgetting `break` statements in `switch` cases, causing unintended fall-through.
* Overcomplicating nested ternary expressions, making code unreadable.

### Best Practices
* Keep `if/else` chains readable or refactor complex conditions into descriptive boolean variables.
* Use `switch` when comparing a single variable against many distinct constant values.

---

## 9. Loops: for, while, do...while, for...of, and for...in

### Definition
Loops repeat blocks of code until a specified condition evaluates to false.

### Syntax
```javascript
// Traditional For Loop
for (let i = 0; i < 3; i++) {
  console.log(`Count: ${i}`);
}

// For...of (Iterates over iterables like arrays)
const colors = ["red", "green", "blue"];
for (const color of colors) {
  console.log(color);
}

// For...in (Iterates over object keys)
const user = { name: "Alice", age: 30 };
for (const key in user) {
  console.log(key, user[key]);
}
```

### Output / Behavior
Iterates through arrays, objects, or counters iteratively.

### Explanation
* `for...of` is ideal for arrays and strings.
* `for...in` is designed for enumerating object properties.
* `while` and `do...while` are best when the number of iterations is unknown beforehand.

### Common Mistakes
* Creating infinite loops by failing to update the loop termination condition.
* Using `for...in` on arrays (which iterates over indices/keys rather than values, and can include inherited properties).

### Best Practices
* Prefer array iteration methods (`map`, `filter`, `forEach`) or `for...of` over traditional `for` loops for cleaner array processing.
* Ensure loop termination conditions are clearly defined.

---

## 10. Functions, parameters, arguments, return values, arrow functions, callbacks, and default parameters

### Definition
Functions are reusable blocks of code designed to perform specific tasks. Arrow functions offer a concise syntax. Callbacks are functions passed as arguments to other functions.

### Syntax
```javascript
// Function Declaration with default parameter
function greet(name = "Guest") {
  return `Hello, ${name}`;
}

// Arrow Function
const add = (a, b) => a + b;

// Callback Example
function processUser(callback) {
  callback("Alice");
}
processUser((name) => console.log(`Processed ${name}`));
```

### Output / Behavior
Computes and returns values or executes callbacks.

### Explanation
Parameters are variables listed in a function definition; arguments are the actual values passed into the function. Functions return values using the `return` keyword; if omitted, they return `undefined`.

### Common Mistakes
* Forgetting the `return` statement in a multi-line arrow function.
* Confusing parameters (definition) with arguments (invocation).

### Best Practices
* Keep functions small, pure, and focused on a single responsibility.
* Use default parameters to handle missing arguments gracefully.

---

## 11. Arrays, indexing, mutation, iteration, and methods such as map, filter, reduce, find, some, and every

### Definition
Arrays are ordered lists of values. JavaScript provides powerful higher-order array methods to manipulate and query data immutably.

### Syntax
```javascript
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(n => n * 2); // [2, 4, 6, 8, 10]
const evens = numbers.filter(n => n % 2 === 0); // [2, 4]
const sum = numbers.reduce((acc, n) => acc + n, 0); // 15
const found = numbers.find(n => n > 3); // 4
```

### Output / Behavior
Transforms and queries array contents cleanly without mutating original arrays when using functional methods.

### Explanation
* `map()` transforms each element.
* `filter()` selects elements matching a condition.
* `reduce()` accumulates array values into a single result.
* `find()` returns the first matching element.
* `some()` and `every()` return booleans based on tests.

### Common Mistakes
* Mutating arrays directly with methods like `splice()` or direct index assignment when purity is expected.
* Forgetting to return a value inside `.map()` or `.filter()`.

### Best Practices
* Prefer declarative array methods (`map`, `filter`, `reduce`) over imperative `for` loops for data transformation.
* Chain methods logically when needed (e.g., `numbers.filter(...).map(...)`).

---

## 12. Objects, properties, methods, destructuring, spread syntax, and optional chaining

### Definition
Objects store collections of key-value pairs. Destructuring unpacks values, spread (`...`) copies/merges, and optional chaining (`?.`) prevents runtime errors when accessing deeply nested properties.

### Syntax
```javascript
const user = {
  name: "Alice",
  address: { city: "New York" }
};

// Destructuring & Optional Chaining
const { name, address: { city } = {} } = user;
const zip = user?.address?.zipCode; // undefined instead of error

// Spread Syntax
const updatedUser = { ...user, age: 25 };
```

### Output / Behavior
Accesses, unpacks, and merges object properties safely.

### Explanation
Optional chaining (`?.`) short-circuits evaluation and returns `undefined` if an intermediate property is `null` or `undefined`. Spread syntax (`...`) creates shallow copies of objects.

### Common Mistakes
* Trying to access nested properties on `undefined` without optional chaining, crashing the script.
* Assuming spread syntax creates deep copies (it only creates shallow copies).

### Best Practices
* Use optional chaining when dealing with unpredictable API responses or deep object structures.
* Use object destructuring to extract needed properties cleanly at the top of functions.

---

## 13. Scope, lexical scope, closures, hoisting, and the temporal dead zone

### Definition
* **Scope:** Visibility of variables.
* **Lexical Scope:** Inner functions have access to variables declared in their outer enclosing scope.
* **Closure:** A function bundled together with references to its lexical environment.
* **Hoisting:** JavaScript's behavior of moving declarations to the top of their scope during compilation.
* **Temporal Dead Zone (TDZ):** The period between entering scope and being declared where `let` and `const` variables cannot be accessed.

### Syntax
```javascript
function makeCounter() {
  let count = 0;
  return function() {
    count++;
    return count;
  };
}
const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```

### Output / Behavior
Maintains private state across function calls using closures.

### Explanation
Closures allow functions to "remember" and access variables from an outer scope even after that outer function has finished executing. `var` declarations are hoisted with `undefined`, whereas `let` and `const` are hoisted into the TDZ.

### Common Mistakes
* Accidental global variables created by omitting `let`/`const`.
* Trying to access `let` or `const` variables before their declaration line.

### Best Practices
* Declare all variables at the top of their scope or right before use to avoid TDZ confusion.
* Leverage closures for data privacy and encapsulation.

---

## 14. DOM selection and manipulation, text content, attributes, classes, and styles

### Definition
The Document Object Model (DOM) is an object representation of the HTML page, allowing JavaScript to dynamically read and modify page content and structure.

### Syntax
```javascript
// Selection
const button = document.querySelector("#submit-btn");
const items = document.querySelectorAll(".list-item");

// Manipulation
button.textContent = "Click Me Now";
button.classList.add("btn-primary");
button.setAttribute("data-action", "save");
button.style.backgroundColor = "blue";
```

### Output / Behavior
Updates element text, adds CSS classes, manages attributes, and modifies inline styles directly in the browser DOM.

### Explanation
`querySelector` returns the first matching element, while `querySelectorAll` returns a static NodeList of all matches. Modifying `textContent` is safer than `innerHTML` when handling untrusted user input.

### Common Mistakes
* Using `document.write()`, which overwrites the entire document.
* Using `innerHTML` with raw user input, creating security vulnerabilities.

### Best Practices
* Cache DOM selections in variables if they are accessed multiple times to improve performance.
* Use `classList.add()` / `classList.remove()` instead of direct `style` manipulation for cleaner separation of concerns.

---

## 15. Events, event listeners, event objects, bubbling, capturing, and delegation

### Definition
Events are actions that happen in the browser (e.g., clicks, keypresses, load). Event listeners respond to these events. Event bubbling propagates events from target elements up to ancestors. Event delegation attaches a single listener to a parent element to handle events for all current and future child elements.

### Syntax
```javascript
const form = document.querySelector("#myForm");

form.addEventListener("click", (event) => {
  event.preventDefault(); // Stop default browser behavior
  console.log("Clicked target:", event.target);
});
```

### Output / Behavior
Captures user interaction events and executes callback handlers.

### Explanation
Event delegation is efficient because you don't need to attach individual listeners to hundreds of list items; a single listener on the parent container handles clicks using `event.target`.

### Common Mistakes
* Forgetting to call `event.preventDefault()` on form submissions, causing page reloads.
* Memory leaks caused by failing to remove event listeners on dynamically destroyed elements.

### Best Practices
* Use event delegation for lists and dynamic elements.
* Always inspect `event.target` safely inside delegated event handlers.

---

## 16. Form handling, input validation, and safe display of user-provided text

### Definition
Form handling involves capturing user inputs, validating data against rules, and safely rendering output to prevent injection attacks.

### Syntax
```javascript
const inputField = document.querySelector("#username");
const outputDiv = document.querySelector("#output");

function handleSubmit(event) {
  event.preventDefault();
  const value = inputField.value.trim();
  
  if (value.length < 3) {
    alert("Username must be at least 3 characters.");
    return;
  }
  
  // Safe display using textContent
  outputDiv.textContent = value;
}
```

### Output / Behavior
Validates input length and safely displays user text without executing embedded HTML/JS.

### Explanation
Never trust client input. Always sanitize and validate on both client and server sides. Use `textContent` instead of `innerHTML` when displaying user input to prevent Cross-Site Scripting (XSS).

### Common Mistakes
* Using `innerHTML` to display user inputs, which exposes the app to XSS attacks.
* Skipping client-side input trimming (`.trim()`).

### Best Practices
* Always trim whitespace from text inputs before validation.
* Use `textContent` for rendering user text securely.

---

## 17. JSON, parsing, serialization, and working with API responses

### Definition
JSON (JavaScript Object Notation) is a lightweight data-interchange format. Serialization converts objects to JSON strings (`JSON.stringify()`), and parsing converts JSON strings to JavaScript objects (`JSON.parse()`).

### Syntax
```javascript
const user = { id: 1, name: "Alice" };

// Serialization (Object to JSON string)
const jsonString = JSON.stringify(user);

// Parsing (JSON string to Object)
const parsedObject = JSON.parse(jsonString);

console.log(parsedObject.name);
```

### Output / Behavior
```text
Alice
```

### Explanation
APIs communicate primarily using JSON strings. `JSON.stringify()` and `JSON.parse()` bridge the gap between JavaScript objects in memory and string-based network transmission.

### Common Mistakes
* Calling `JSON.parse()` on data that is already a JavaScript object.
* Attempting to parse malformed JSON strings, which throws a syntax error.

### Best Practices
* Wrap `JSON.parse()` calls inside `try...catch` blocks when handling untrusted API responses or local storage data.

---

## 18. Error handling using try, catch, finally, and throwing errors

### Definition
Error handling allows developers to gracefully catch and manage runtime exceptions without crashing the entire application.

### Syntax
```javascript
function divide(a, b) {
  try {
    if (b === 0) {
      throw new Error("Division by zero is not allowed.");
    }
    return a / b;
  } catch (error) {
    console.error("Caught error:", error.message);
  } finally {
    console.log("Execution complete.");
  }
}
divide(10, 0);
```

### Output / Behavior
```text
Caught error: Division by zero is not allowed.
Execution complete.
```

### Explanation
The `try` block wraps risky code, `catch` handles any thrown errors, and `finally` executes cleanup code regardless of whether an error occurred.

### Common Mistakes
* Catching errors silently with empty `catch {}` blocks, hiding critical bugs.
* Throwing primitive strings instead of native `Error` objects (`throw new Error(...)`).

### Best Practices
* Always throw `Error` objects for stack trace tracking.
* Log errors meaningfully or present user-friendly fallback messages.

---

## 19. ES modules, imports, exports, and code organization

### Definition
ES Modules (ESM) allow developers to split JavaScript code into separate, reusable files using `export` and `import` statements.

### Syntax
```javascript
// math.js
export const add = (a, b) => a + b;
export default function subtract(a, b) { return a - b; }

// main.js
import subtract, { add } from './math.js';
console.log(add(2, 3));
```

### Output / Behavior
Imports functions across files cleanly. HTML script tags must include `type="module"`.

### Explanation
Modules have their own private scope, preventing global namespace pollution. You can export multiple named exports and one default export per file.

### Common Mistakes
* Forgetting `type="module"` in the HTML script tag when running in browsers.
* Incorrect relative file paths in import statements.

### Best Practices
* Group related code into modular files (e.g., `api.js`, `ui.js`, `utils.js`).
* Use named exports for utility libraries and default exports for primary components/classes.

---

## 20. Asynchronous JavaScript: callbacks, promises, async, await, and the event loop at an introductory level

### Definition
JavaScript is single-threaded. Asynchronous operations (like timers or network requests) are handled non-blockingly using the Event Loop, Callbacks, Promises, and `async/await`.

### Syntax
```javascript
const fetchData = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data loaded"), 1000);
  });
};

async function run() {
  const result = await fetchData();
  console.log(result);
}
run();
```

### Output / Behavior
Waits 1st second asynchronously, then logs `"Data loaded"`.

### Explanation
The event loop continuously checks the call stack and message/microtask queues. Promises represent eventual completion of asynchronous operations, and `async/await` provides clean, synchronous-looking syntax for working with promises.

### Common Mistakes
* Forgetting the `await` keyword before a promise-returning function.
* Falling into "Callback Hell" by nesting multiple callbacks deeply.

### Best Practices
* Prefer `async/await` over raw promise chains (`.then().catch()`) for readability.
* Always handle asynchronous errors using `try...catch`.

---

## 21. Fetch API, HTTP basics, response status codes, JSON APIs, and error handling

### Definition
The `Fetch API` provides an interface for fetching resources across the network via HTTP requests.

### Syntax
```javascript
async function getUserData(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Fetch failed:", error.message);
  }
}
```

### Output / Behavior
Sends HTTP GET requests, checks response status codes (e.g., `200 OK`, `404 Not Found`), and parses JSON.

### Explanation
`fetch()` returns a promise that resolves to the `Response` object. Note that `fetch()` only rejects on network failures, not on HTTP error status codes like 404 or 500—hence checking `response.ok` is mandatory.

### Common Mistakes
* Forgetting to check `response.ok` before calling `.json()`.
* Forgetting to `await` both `fetch()` and `.json()`.

### Best Practices
* Always wrap `fetch` calls in `try...catch` and check `response.ok`.
* Show loading states to users while waiting for network responses.

---

## 22. Local storage, session storage, their limitations, and avoiding storage of sensitive information

### Definition
Web Storage APIs (`localStorage` and `sessionStorage`) allow key-value data persistence in the browser. `localStorage` persists until cleared; `sessionStorage` clears when the browser tab closes.

### Syntax
```javascript
// Save data
localStorage.setItem("theme", "dark");

// Retrieve data
const currentTheme = localStorage.getItem("theme");

// Remove data
localStorage.removeItem("theme");
```

### Output / Behavior
Persists data across page reloads in the browser storage.

### Explanation
Both storages store data *only as strings*. They are synchronous and limited to ~5MB. They are accessible by any script running on the same origin, making them insecure for sensitive credentials.

### Common Mistakes
* Storing sensitive tokens (like raw passwords or high-security JWTs) in `localStorage` where XSS attacks can steal them.
* Storing objects directly without `JSON.stringify()`.

### Best Practices
* Never store sensitive user secrets or passwords in `localStorage`.
* Always use `JSON.stringify()` and `JSON.parse()` when storing complex objects or arrays.

---

## 23. Classes, constructors, prototypes, inheritance, encapsulation, and object-oriented programming

### Definition
Classes serve as blueprints for creating objects with shared properties and methods using Object-Oriented Programming (OOP) principles in JavaScript.

### Syntax
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    return `Hello, my name is ${this.name}`;
  }
}

class Student extends Person {
  constructor(name, grade) {
    super(name);
    this.grade = grade;
  }
}

const student = new Student("Alice", "A");
```

### Output / Behavior
Instantiates objects inheriting properties and methods from parent classes.

### Explanation
JavaScript classes are syntactical sugar over prototype-based inheritance. `extends` enables inheritance, and `super()` calls the parent constructor.

### Common Mistakes
* Forgetting to call `super()` inside a subclass constructor before using `this`.
* Misunderstanding that JS uses prototype delegation under the hood rather than classical OOP.

### Best Practices
* Use classes for structuring complex components, data models, or state managers.
* Keep methods clean and leverage encapsulation.

---

## 24. Functional programming concepts, pure functions, immutability, and reusable logic

### Definition
Functional programming (FP) treats computation as the evaluation of mathematical functions, avoiding mutable state and side effects.

### Syntax
```javascript
// Pure function (same input always produces same output, no side effects)
const addTax = (price) => price * 1.2;

// Immutable update of an array
const addItem = (list, item) => [...list, item];
```

### Output / Behavior
Computes outputs deterministically without modifying outer state or variables.

### Explanation
Pure functions make code easier to test, debug, and reason about. Immutability ensures data structures are never modified in place, preventing unintended side effects.

### Common Mistakes
* Writing impure functions that modify global variables or mutate argument objects directly.
* Relying on random numbers or current timestamps inside functions tested for purity.

### Best Practices
* Write pure functions whenever possible, separating business logic from side effects (like DOM updates or API calls).
* Use spread syntax (`...`) to achieve immutability when updating state objects and arrays.

---

## 25. Regular expressions and common validation examples

### Definition
Regular Expressions (RegEx) are patterns used to match character combinations in strings for searching, formatting, and validation.

### Syntax
```javascript
const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
const isValidEmail = emailRegex.test("test@example.com");

console.log(isValidEmail);
```

### Output / Behavior
```text
true
```

### Explanation
The `.test()` method returns a boolean indicating whether the string matches the regex pattern. RegEx uses special characters like `^` (start), `$` (end), `[]` (character sets), and `+` (quantifiers).

### Common Mistakes
* Writing overly complex, unreadable regular expressions.
* Forgetting anchoring characters (`^` and `$`), leading to partial matches.

### Best Practices
* Use well-tested standard regex patterns for common validations like emails or postal codes.
* Comment complex regular expressions or test them thoroughly using online visualizers.

---

## 26. Browser security basics, XSS, safe DOM methods, and why client-side validation is not sufficient for security

### Definition
Browser security involves protecting web applications from vulnerabilities such as Cross-Site Scripting (XSS). Client-side validation improves user experience but can easily be bypassed; server-side validation is mandatory for security.

### Syntax & Explanation
* **XSS Prevention:** Avoid `innerHTML` with user input. Use `textContent` instead.
* **Why Client Validation Fails:** Users can disable JavaScript, use cURL, or modify network requests directly in developer tools.

### Common Mistakes
* Relying solely on client-side form validation for authentication or database security.
* Rendering raw user-submitted comments using `innerHTML`.

### Best Practices
* Always validate and sanitize data on the server side regardless of client-side validation.
* Encode or use safe DOM methods (`textContent`) to neutralize malicious scripts.

---

## 27. Debugging, testing fundamentals, linting, performance, and common errors

### Definition
Debugging is the process of identifying and fixing bugs. Testing ensures code correctness. Linting (e.g., ESLint) enforces code quality and style standards.

### Syntax & Tools
```javascript
// Debugging using console tools
console.table([{ name: "Alice" }, { name: "Bob" }]);
debugger; // Pauses execution in browser dev tools
```

### Output / Behavior
Pauses execution at the `debugger` statement when developer tools are open, allowing step-by-step inspection.

### Explanation
Effective debugging utilizes `console.log`, `console.table`, and browser breakpoint tools. Unit testing frameworks like Jest or Vitest verify individual units of code.

### Common Mistakes
* Leaving `console.log` statements cluttering production codebases.
* Ignoring linter warnings.

### Best Practices
* Use linters and formatters (like ESLint and Prettier) in your development workflow.
* Write unit tests for critical business logic.

---

## 28. Modern JavaScript features and compatibility considerations

### Definition
Modern JavaScript (ES6+) introduces powerful features that improve developer ergonomics. Transpilers like Babel convert modern JS into backwards-compatible code for older browsers.

### Syntax
```javascript
// Optional Chaining & Nullish Coalescing
const config = user?.settings?.theme ?? "light";
```

### Output / Behavior
Provides fallback values when properties are `null` or `undefined`.

### Explanation
The nullish coalescing operator (`??`) returns the right-hand operand when the left-hand operand is `null` or `undefined` (unlike `||`, which triggers on all falsy values like `0` or `""`).

### Common Mistakes
* Using cutting-edge JavaScript features in production without checking browser support or setting up a build tool (like Vite or Babel).

### Best Practices
* Use modern ES6+ features paired with modern bundlers for optimal developer experience and performance.

---

## Complete Practical Examples

### 1. A Counter
```html
<div>
  <span id="counter-value">0</span>
  <button id="decrement">-</button>
  <button id="increment">+</button>
</div>
<script>
  let count = 0;
  const valueEl = document.getElementById("counter-value");
  
  document.getElementById("increment").addEventListener("click", () => {
    count++;
    valueEl.textContent = count;
  });
  
  document.getElementById("decrement").addEventListener("click", () => {
    count--;
    valueEl.textContent = count;
  });
</script>
```

### 2. A Calculator
```javascript
function calculate(num1, operator, num2) {
  switch (operator) {
    case "+": return num1 + num2;
    case "-": return num1 - num2;
    case "*": return num1 * num2;
    case "/": return num2 !== 0 ? num1 / num2 : "Error: Division by zero";
    default: return "Invalid operator";
  }
}
console.log(calculate(10, "+", 5)); // 15
```

### 3. Form Validation
```javascript
const form = document.querySelector("#signup-form");
form.addEventListener("submit", (e) => {
  e.preventDefault();
  const email = document.querySelector("#email").value.trim();
  const errorEl = document.querySelector("#error-msg");
  
  if (!email.includes("@")) {
    errorEl.textContent = "Please enter a valid email address.";
    return;
  }
  errorEl.textContent = "";
  alert("Form submitted successfully!");
});
```

### 4. A To-Do List
```javascript
const todos = [];
function addTodo(taskText) {
  todos.push({ id: Date.now(), text: taskText, completed: false });
}
function toggleTodo(id) {
  const todo = todos.find(t => t.id === id);
  if (todo) todo.completed = !todo.completed;
}
addTodo("Learn JavaScript");
console.log(todos);
```

### 5. A Searchable List
```javascript
const items = ["Apple", "Banana", "Cherry", "Date"];
function searchItems(query) {
  return items.filter(item => item.toLowerCase().includes(query.toLowerCase()));
}
console.log(searchItems("ap")); // ["Apple"]
```

### 6. A Theme Toggle
```javascript
const toggleBtn = document.querySelector("#theme-toggle");
toggleBtn.addEventListener("click", () => {
  document.body.classList.toggle("dark-theme");
  const isDark = document.body.classList.contains("dark-theme");
  localStorage.setItem("theme", isDark ? "dark" : "light");
});
```

### 7. Fetching Data from a Public API
```javascript
async function fetchJoke() {
  try {
    const response = await fetch("https://api.chucknorris.io/jokes/random");
    if (!response.ok) throw new Error("Network response failed");
    const data = await response.json();
    console.log(data.value);
  } catch (error) {
    console.error("Error fetching joke:", error);
  }
}
fetchJoke();
```

### 8. A Small Application Using Modules
```javascript
// utils.js
export const formatCurrency = (amount) => `$${amount.toFixed(2)}`;

// app.js
import { formatCurrency } from './utils.js';
console.log(formatCurrency(49.99)); // "$49.99"
```

---

## Glossary
* **API:** Application Programming Interface; a set of rules allowing programs to communicate.
* **Callback:** A function passed into another function as an argument to be executed later.
* **Closure:** A function that retains access to its outer lexical scope even after the outer function has closed.
* **DOM:** Document Object Model; an object-oriented representation of a web page.
* **Hoisting:** JavaScript mechanism where variable and function declarations are moved to the top of their scope during compilation.
* **Immutable:** Unchanging over time or unable to be changed.
* **JSON:** JavaScript Object Notation; a lightweight data interchange format.
* **Promise:** An object representing the eventual completion or failure of an asynchronous operation.
* **Prototype:** The mechanism by which JavaScript objects inherit features from one another.
* **XSS:** Cross-Site Scripting; a vulnerability where malicious scripts are injected into trusted websites.

---

## 25 Interview Questions with Answers

1. **Q: What is the difference between `let`, `const`, and `var`?**
   * **A:** `var` is function-scoped and hoisted with `undefined`. `let` and `const` are block-scoped and hoisted into the temporal dead zone. `const` cannot be reassigned, whereas `let` can.
2. **Q: Explain closures in JavaScript.**
   * **A:** A closure is a function that remembers and has access to variables in its outer lexical scope even after that outer function has finished executing.
3. **Q: What is event bubbling and event capturing?**
   * **A:** Event bubbling propagates events from the target element up to its ancestors. Event capturing propagates events from the outermost ancestor down to the target element.
4. **Q: What is the difference between `==` and `===`?**
   * **A:** `==` performs type coercion before comparing values, whereas `===` (strict equality) requires both value and data type to be identical.
5. **Q: How does the Event Loop work?**
   * **A:** The event loop monitors the call stack and message/microtask queues, executing asynchronous callbacks when the call stack is empty.
6. **Q: What are arrow functions and how do they differ from regular functions?**
   * **A:** Arrow functions provide a concise syntax and do not have their own `this`, `arguments`, or `super` bindings; `this` is lexically inherited.
7. **Q: What is NaN in JavaScript?**
   * **A:** "Not-a-Number" represents a computational error resulting from an invalid number operation. `typeof NaN` is `"number"`.
8. **Q: Explain prototypal inheritance.**
   * **A:** Objects in JavaScript inherit properties and methods from a prototype object through the prototype chain.
9. **Q: What is the Temporal Dead Zone (TDZ)?**
   * **A:** The period between entering scope and a `let` or `const` variable declaration where accessing the variable throws a `ReferenceError`.
10. **Q: What is event delegation?**
    * **A:** A technique where a single event listener is attached to a parent element to manage events for all current and future child elements using event bubbling.
11. **Q: What is the difference between `null` and `undefined`?**
    * **A:** `undefined` means a variable has been declared but not assigned a value. `null` is an assignment value representing intentional absence of any object value.
12. **Q: How do you perform asynchronous operations in JavaScript?**
    * **A:** Using Callbacks, Promises, and `async/await` syntax.
13. **Q: What are higher-order functions?**
    * **A:** Functions that take other functions as arguments, return functions, or both (e.g., `map`, `filter`).
14. **Q: What is CORS?**
    * **A:** Cross-Origin Resource Sharing; an HTTP-header based mechanism that allows a server to indicate any origins other than its own from which a browser should permit loading resources.
15. **Q: Explain destructuring assignment.**
    * **A:** A syntax that allows unpacking values from arrays or properties from objects into distinct variables.
16. **Q: What is short-circuit evaluation?**
    * **A:** An evaluation technique in logical expressions (`&&`, `||`) where the compiler stops evaluating as soon as the result is determined.
17. **Q: Why is client-side validation insufficient for security?**
    * **A:** Because users can bypass browser checks, modify network requests, or disable JavaScript entirely. Server-side validation is mandatory.
18. **Q: What is local storage versus session storage?**
    * **A:** `localStorage` persists data across browser sessions until explicitly cleared. `sessionStorage` clears data when the specific browser tab or window is closed.
19. **Q: What is an IIFE?**
    * **A:** Immediately Invoked Function Expression; a function defined as an expression that executes immediately upon creation.
20. **Q: What is a pure function?**
    * **A:** A function that, given the same inputs, always returns the same output and produces no side effects.
21. **Q: How do you handle errors in asynchronous code using `async/await`?**
    * **A:** By wrapping the code inside a `try...catch` block.
22. **Q: What is the purpose of the `fetch()` API?**
    * **A:** To make asynchronous HTTP requests across the network and handle responses programmatically.
23. **Q: What is optional chaining?**
    * **A:** The `?.` operator that safely accesses nested object properties without throwing an error if an intermediate reference is `null` or `undefined`.
24. **Q: What is an ES module?**
    * **A:** JavaScript's official module system for organizing and sharing code between files using `import` and `export`.
25. **Q: What is strict mode in JavaScript?**
    * **A:** A mode (`"use strict";`) that opts in to a stricter parsing and error-handling variant of JavaScript, catching common coding errors and silent bugs.

---

## 25 MCQs with Answer Key

1. Which keyword declares a block-scoped variable that cannot be reassigned?
   - A) `var`
   - B) `let`
   - C) `const`
   - D) `function`
2. What does `typeof null` return in JavaScript?
   - A) `"null"`
   - B) `"undefined"`
   - C) `"object"`
   - D) `"number"`
3. Which array method creates a new array with all elements passing a test?
   - A) `map()`
   - B) `filter()`
   - C) `reduce()`
   - D) `forEach()`
4. What is the output of `typeof NaN`?
   - A) `"NaN"`
   - B) `"undefined"`
   - C) `"number"`
   - D) `"object"`
5. Which operator is used for strict equality comparison?
   - A) `=`
   - B) `==`
   - C) `===`
   - D) `equals`
6. Which method converts a JavaScript object into a JSON string?
   - A) `JSON.parse()`
   - B) `JSON.stringify()`
   - C) `JSON.convert()`
   - D) `JSON.toStr()`
7. What scope do `let` and `const` variables have?
   - A) Global scope
   - B) Function scope
   - C) Block scope
   - D) Module scope only
8. Which method stops default browser behavior on an event?
   - A) `event.stop()`
   - B) `event.preventDefault()`
   - C) `event.cancel()`
   - D) `event.stopPropagation()`
9. What does `Array.prototype.reduce()` return?
   - A) A new array
   - B) A boolean
   - C) A single accumulated value
   - D) An object
10. Which storage mechanism persists data even after closing the browser tab?
    - A) `sessionStorage`
    - B) `localStorage`
    - C) `MemoryStorage`
    - D) `CookieStorage`
11. Which symbol is used for template literals?
    - A) Single quote (`'`)
    - B) Double quote (`"`)
    - C) Backtick (`` ` ``)
    - D) Hash (`#`)
12. What does `Math.floor(4.9)` evaluate to?
    - A) 5
    - B) 4
    - C) 4.9
    - D) 0
13. Which event listener property enables event delegation?
    - A) `event.target`
    - B) `event.currentTarget`
    - C) `event.bubbles`
    - D) `event.path`
14. How do you catch errors in an `async/await` function?
    - A) `.catch()` only
    - B) `try...catch` block
    - C) `error` keyword
    - D) `throw` block
15. Which statement about arrow functions is correct?
    - A) They have their own `this` keyword.
    - B) They cannot return values implicitly.
    - C) They do not have their own `this` binding.
    - D) They can be used as constructors with `new`.
16. Which method finds the first element matching a condition in an array?
    - A) `filter()`
    - B) `find()`
    - C) `some()`
    - D) `every()`
17. What does `response.ok` check in the Fetch API?
    - A) If status is in the range 200–299
    - B) If the network cable is connected
    - C) If JSON parsing succeeded
    - D) If CORS is enabled
18. What is the purpose of optional chaining (`?.`)?
    - A) To speed up execution
    - B) To prevent errors when accessing nested properties on null/undefined
    - C) To chain array methods
    - D) To declare optional function parameters
19. Which HTML attribute is required to load ES modules via script tags?
    - A) `async`
    - B) `defer`
    - C) `type="module"`
    - D) `crossorigin`
20. What is the result of `Boolean(0)`?
    - A) `true`
    - B) `false`
    - C) `undefined`
    - D) `null`
21. Which method removes whitespace from both ends of a string?
    - A) `strip()`
    - B) `trim()`
    - C) `clean()`
    - D) `slice()`
22. What causes the Temporal Dead Zone?
    - A) Using `var` declarations
    - B) Accessing `let` or `const` before their declaration
    - C) Infinite loops
    - D) Network latency
23. Which operator is the nullish coalescing operator?
    - A) `&&`
    - B) `||`
    - C) `??`
    - D) `?`
24. What is the output of `console.log(typeof ([]))`?
    - A) `"array"`
    - B) `"list"`
    - C) `"object"`
    - D) `"undefined"`
25. Which security vulnerability involves injecting malicious scripts into web pages?
    - A) CSRF
    - B) SQL Injection
    - C) XSS (Cross-Site Scripting)
    - D) DDOS

### Answer Key
1. C | 2. C | 3. B | 4. C | 5. C | 6. B | 7. C | 8. B | 9. C | 10. B | 11. C | 12. B | 13. A | 14. B | 15. C | 16. B | 17. A | 18. B | 19. C | 20. B | 21. B | 22. B | 23. C | 24. C | 25. C

---

## Five Projects Ordered by Difficulty

1. **Project 1 (Beginner): Interactive Tip Calculator**
   - *Description:* Build a web app that calculates tip and total split amounts based on bill input and tip percentage buttons.
   - *Concepts:* DOM selection, event listeners, basic arithmetic, and template literals.

2. **Project 2 (Beginner-Intermediate): LocalStorage To-Do List**
   - *Description:* A task management app where users can add, delete, mark tasks as complete, and persist data in `localStorage`.
   - *Concepts:* Arrays, higher-order methods (`filter`, `map`), DOM manipulation, event delegation, and Web Storage API.

3. **Project 3 (Intermediate): Weather Dashboard with Fetch API**
   - *Description:* An application that fetches weather data from a public API based on user search input and displays current conditions.
   - *Concepts:* `async/await`, `fetch`, error handling (`try...catch`), JSON parsing, and UI loading states.

4. **Project 4 (Advanced): Kanban Task Board with Drag and Drop**
   - *Description:* A fully interactive board where tasks can be moved across columns (Todo, In Progress, Done) with state persistence.
   - *Concepts:* Advanced DOM drag-and-drop events, object-oriented or modular state management, and ES modules.

5. **Project 5 (Advanced): Real-Time Markdown Notes App**
   - *Description:* A note-taking application featuring live Markdown preview rendering, local storage auto-saving, tag filtering, and search functionality.
   - *Concepts:* Regular expressions, string parsing, event handling, modular architecture, and performance optimization.