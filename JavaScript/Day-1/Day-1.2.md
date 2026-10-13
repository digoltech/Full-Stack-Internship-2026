# Day 1.2 — Hoisting, Execution Context, and Call Stack

## 1. Learning Objectives

By the end of this session, you should be able to:

- Explain hoisting in JavaScript.
- Understand how `var`, `let`, and `const` behave before initialization.
- Explain the Temporal Dead Zone.
- Differentiate between function declarations and function expressions.
- Understand execution context.
- Trace function calls using the call stack.
- Debug initialization and function-call errors.

## 2. Topics Covered

1. What hoisting means
2. Hoisting with `var`
3. Hoisting with `let` and `const`
4. The Temporal Dead Zone
5. Function declaration hoisting
6. Function expressions and initialization
7. Execution context
8. The call stack
9. Debugging common execution errors

---

## Topic 1: What Is Hoisting?

Before executing JavaScript statements, the JavaScript engine processes declarations in their relevant scopes.

This behavior is commonly described as **hoisting**.

Hoisting does not mean that JavaScript literally moves every declaration to the top of your source file. It is a way of describing how declarations are handled during execution.

Different declarations behave differently.

---

## Topic 2: Hoisting with `var`

Consider this example:

```js
console.log(score);

var score = 50;

console.log(score);
```

Output:

```text
undefined
50
```

### Why Does This Happen?

The declaration of `score` is processed before the assignment executes. The variable initially has the value `undefined`.

When JavaScript reaches `score = 50`, the variable receives its assigned value.

A simplified mental model is:

```js
var score;

console.log(score);

score = 50;

console.log(score);
```

This model helps explain the behavior, but it is not a literal transformation of the source code.

### Another Example

```js
var studentName = "Asha";

function showName() {
  console.log(studentName);
}

showName();
```

Output:

```text
Asha
```

The function reads the variable from its outer scope.

### Predict the Output

```js
console.log(price);

var price = 500;

console.log(price);

price = 800;

console.log(price);
```

Write your answer before running the program.

---

## Topic 3: Hoisting with `let` and `const`

Variables declared with `let` and `const` behave differently from `var`.

They are associated with their scope before execution reaches their declaration, but they cannot be accessed until they are initialized.

```js
console.log(total);

let total = 500;
```

Result:

```text
ReferenceError
```

The error occurs because the variable is in the **Temporal Dead Zone** when the first statement runs.

### Another Example

```js
console.log(course);

const course = "MERN Stack";
```

This also produces a `ReferenceError`.

### Compare the Three

```js
console.log(a);
var a = 10;

console.log(b);
let b = 20;

console.log(c);
const c = 30;
```

The program stops at the first `ReferenceError`, so it will not execute all the way through.

To observe the behavior independently, run each example separately.

| Declaration | Access before initialization |
|---|---|
| `var` | Returns `undefined` |
| `let` | Throws `ReferenceError` |
| `const` | Throws `ReferenceError` |

---

## Topic 4: Temporal Dead Zone (TDZ)

The **Temporal Dead Zone** is the period from entering the scope of a `let` or `const` declaration until that variable is initialized.

### Example

```js
{
  // The variable is in its TDZ here.

  let message = "Hello";

  console.log(message);
}
```

Output:

```text
Hello
```

The variable can be accessed after initialization.

### Example with an Error

```js
{
  console.log(message);

  let message = "Hello";
}
```

This throws a `ReferenceError`.

### Why Is the TDZ Useful?

It helps prevent accidental use of variables before they have been initialized.

This behavior is one reason `let` and `const` are generally easier to reason about than `var`.

### Task

For each example, identify whether the variable is:

- Not declared in the relevant scope.
- Declared with `var` but not yet assigned.
- In the Temporal Dead Zone.
- Initialized and ready to use.

---

## Topic 5: Function Declaration Hoisting

A function declaration can generally be called before its position in the source code.

```js
greet();

function greet() {
  console.log("Hello, developer!");
}
```

Output:

```text
Hello, developer!
```

The function declaration is available when the code executes the call.

### Another Example

```js
console.log(add(5, 7));

function add(a, b) {
  return a + b;
}
```

Output:

```text
12
```

### Important Difference

This behavior applies to function declarations. It does not mean every function assigned to a variable can be called before initialization.

---

## Topic 6: Function Expressions and Hoisting

A function expression assigns a function to a variable.

```js
const greet = function () {
  console.log("Hello!");
};

greet();
```

Output:

```text
Hello!
```

### Calling It Before Initialization

```js
greet();

const greet = function () {
  console.log("Hello!");
};
```

This produces a `ReferenceError` because `greet` is a `const` variable that has not yet been initialized.

### Compare the Examples

**Function declaration**

```js
sayHello();

function sayHello() {
  console.log("Hello");
}
```

**Function expression**

```js
// sayHello(); // ReferenceError if executed here

const sayHello = function () {
  console.log("Hello");
};

sayHello();
```

### Task

Create two functions that calculate the square of a number:

1. One using a function declaration.
2. One using a function expression.

Test whether each can be called before its definition or initialization. Explain the result.

---

## Topic 7: Execution Context

An **execution context** is the environment in which JavaScript code runs.

For this session, focus on:

- The global execution context.
- Function execution contexts.

### Global Execution Context

When JavaScript starts executing a script, it creates an environment for the top-level code.

```js
const course = "MERN Stack";

console.log(course);
```

The top-level code executes in its surrounding execution environment.

### Function Execution Context

When a function is called, JavaScript creates a function execution context for that call.

```js
function calculateTotal(price, quantity) {
  const total = price * quantity;

  return total;
}

const result = calculateTotal(100, 3);

console.log(result);
```

Output:

```text
300
```

The function call has its own parameters and local variables.

When the function returns, execution continues in the calling context.

### Understanding the Flow

1. The top-level script begins executing.
2. JavaScript reaches `calculateTotal(100, 3)`.
3. The function is called with `price = 100` and `quantity = 3`.
4. The function calculates `total`.
5. The function returns `300`.
6. The calling code stores the returned value in `result`.
7. The console prints `300`.

### Task

Write a function called `calculateDiscount(price, percentage)`.

Explain:

- Which values are passed as arguments.
- Which variables are parameters.
- Which variable is local to the function.
- What value the function returns.

---

## Topic 8: The Call Stack

The **call stack** tracks active function calls.

When one function calls another function, the new function is placed above the current function in the stack. When it finishes, control returns to the caller.

### Example

```js
function second() {
  console.log("Inside second");
}

function first() {
  console.log("Inside first");
  second();
  console.log("First finished");
}

console.log("Program starts");

first();

console.log("Program ends");
```

Output:

```text
Program starts
Inside first
Inside second
First finished
Program ends
```

### Explanation

- The program starts.
- `first()` is called.
- `first()` calls `second()`.
- `second()` finishes.
- Execution returns to `first()`.
- `first()` finishes.
- The top-level program continues.

### Call Stack During `second()`

```text
Top
┌──────────────────┐
│ second()         │
├──────────────────┤
│ first()          │
├──────────────────┤
│ top-level script │
└──────────────────┘
Bottom
```

This is a simplified illustration of the active calls.

### Example: Three Nested Calls

```js
function third() {
  console.log("Third");
}

function second() {
  console.log("Second");
  third();
  console.log("Second finished");
}

function first() {
  console.log("First");
  second();
  console.log("First finished");
}

first();
```

Output:

```text
First
Second
Third
Second finished
First finished
```

### Task

Before running the program:

1. Predict the output.
2. Draw the call stack while `third()` is running.
3. Explain which function resumes after `third()` finishes.

---

## Topic 9: Debugging Execution Errors

Consider this program:

```js
console.log(studentName);

let studentName = "Asha";

function displayStudent() {
  const course = "MERN Stack";
}

displayStudent();

console.log(course);
```

### Problems

1. `studentName` is accessed before initialization, so the first access throws a `ReferenceError`.
2. `course` is declared inside `displayStudent()`, so it is not accessible from the top-level scope.

Because the first error stops ordinary execution, the second error is not reached in this run.

### Corrected Version

```js
let studentName = "Asha";

function displayStudent() {
  const course = "MERN Stack";

  console.log(studentName);
  console.log(course);
}

displayStudent();
```

Output:

```text
Asha
MERN Stack
```

### Debugging Practice

Use browser DevTools:

1. Open a browser page.
2. Open Developer Tools.
3. Select the Console tab.
4. Run the examples.
5. Read the complete error message.
6. Identify the line that caused the error.
7. Fix the problem and run the code again.

---

# Day 1.2 — End-of-Session Tasks

## Task 1: Hoisting Experiments

Create separate files demonstrating:

- `var` accessed before assignment.
- `let` accessed before initialization.
- `const` accessed before initialization.
- A function declaration called before its declaration.
- A function expression called before initialization.

Write the expected output or error in a comment.

## Task 2: Function Call Trace

Create three functions:

- `startProcess()`
- `validateData()`
- `saveData()`

Make them call one another in sequence. Print a message before and after each nested call. Draw the call stack at the deepest point.

## Task 3: Debugging

Find and fix the errors:

```js
printMessage();

const message = "Welcome";

function printMessage() {
  console.log(message);
}
```

Explain why the code fails as written and why the function declaration itself is not the issue.

## Task 4: Execution Context Explanation

Write a short explanation of what happens when this code runs:

```js
function add(a, b) {
  const result = a + b;
  return result;
}

const answer = add(10, 20);

console.log(answer);
```

Explain the function call, local variables, return value, and execution order.

---

# Day 1.2 — Review Questions

1. What is hoisting?
2. Does JavaScript literally move all declarations to the top of a file?
3. Why does accessing an uninitialized `var` variable return `undefined`?
4. What happens when a `let` variable is accessed before initialization?
5. What is the Temporal Dead Zone?
6. Can a function declaration be called before its declaration?
7. Can a `const` function expression be called before its variable is initialized?
8. What is an execution context?
9. What is the call stack?
10. What happens when a function calls another function?
11. What happens after a function returns?
12. How would you debug a `ReferenceError`?

## Completion Criteria

Before moving to Day 1.3, you should be able to predict the output of short programs involving hoisting and function calls, then explain your reasoning without relying on memorized answers.
