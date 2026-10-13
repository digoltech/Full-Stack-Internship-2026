# Day 1.1 — JavaScript Basics, Variables, and Scope

## 1. Learning Objectives

By the end of this session, you should be able to:

- Explain how JavaScript executes statements.
- Declare and use variables.
- Understand `var`, `let`, and `const`.
- Explain global scope, function scope, and block scope.
- Identify common scope-related errors.
- Write small programs using variables and conditional blocks.

## 2. Topics Covered

1. Introduction to JavaScript execution
2. Variables and declarations
3. The difference between `var`, `let`, and `const`
4. Global scope
5. Function scope
6. Block scope
7. Scope shadowing
8. Common scope errors

---

## Topic 1: JavaScript Execution Basics

JavaScript is a programming language used to build interactive web applications. Before working with React and Node.js, you need to understand how JavaScript executes code.

For ordinary synchronous code, JavaScript generally executes statements in order, from top to bottom.

### Example

```js
console.log("Starting program");

const name = "Asha";

console.log(name);

console.log("Program finished");
```

### Output

```text
Starting program
Asha
Program finished
```

### Explanation

1. The first `console.log()` prints a message.
2. The variable `name` is initialized with the string `"Asha"`.
3. The next statement prints the value stored in `name`.
4. The last statement prints the completion message.

JavaScript evaluates each statement when execution reaches it. Some advanced features, such as asynchronous operations, can affect when particular callbacks execute; these will be covered later.

### Example: Using Variables

```js
const firstName = "Asha";
const lastName = "Patel";

const fullName = firstName + " " + lastName;

console.log(fullName);
```

Output:

```text
Asha Patel
```

The `+` operator joins strings when its operands are strings.

### Try It Yourself

Create variables for:

- Your name
- Your age
- Your city
- Your current course

Print a sentence using all four values.

---

## Topic 2: Variables and Declarations

A variable is a named binding that allows a program to refer to a value.

JavaScript provides three main declaration keywords:

- `var`
- `let`
- `const`

### 2.1 Using `var`

```js
var studentName = "Rahul";

console.log(studentName);

studentName = "Amit";

console.log(studentName);
```

Output:

```text
Rahul
Amit
```

The value assigned to a `var` variable can be changed.

### 2.2 Using `let`

```js
let marks = 75;

console.log(marks);

marks = 90;

console.log(marks);
```

Output:

```text
75
90
```

Use `let` when a variable needs to be reassigned.

### 2.3 Using `const`

```js
const course = "MERN Stack";

console.log(course);
```

Output:

```text
MERN Stack
```

A `const` binding cannot be reassigned after initialization.

```js
const course = "MERN Stack";

// course = "Python"; // TypeError
```

A `const` declaration must be initialized when it is declared.

```js
// const age; // SyntaxError
```

### 2.4 Choosing the Correct Keyword

Consider a program that tracks completed tasks.

```js
const studentName = "Rahul";
const courseName = "MERN Stack";

let completedTasks = 0;

completedTasks = completedTasks + 1;
completedTasks = completedTasks + 1;

console.log(studentName);
console.log(courseName);
console.log(completedTasks);
```

Output:

```text
Rahul
MERN Stack
2
```

The student's name and course do not need reassignment, so `const` is appropriate. The task count changes, so `let` is appropriate.

**Best practice:** Prefer `const` by default. Use `let` when reassignment is necessary. Avoid `var` in most modern JavaScript application code.

---

## Topic 3: `var`, `let`, and `const` Compared

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Function-scoped | Yes | No | No |
| Block-scoped | No | Yes | Yes |
| Reassignment | Allowed | Allowed | Not allowed |
| Redeclaration in the same scope | Allowed | Not allowed | Not allowed |
| Initialization required at declaration | No | No | Yes |

### Example: Redeclaration

```js
var city = "Anand";
var city = "Ahmedabad";

console.log(city);
```

Output:

```text
Ahmedabad
```

With `let`, declaring another variable with the same name in the same scope produces an error.

```js
let age = 20;

// let age = 25; // SyntaxError
```

However, a variable declared in a nested block can have the same name as an outer variable. This is called **shadowing**, which is covered later.

### Important: `const` Does Not Freeze Objects

```js
const student = {
  name: "Rahul",
  marks: 75
};

student.marks = 90;

console.log(student.marks);
```

Output:

```text
90
```

Changing the object's property is allowed. Reassigning the variable is not.

```js
// student = {}; // TypeError
```

`const` prevents reassignment of the binding; it does not automatically make the referenced object immutable.

### Practice

Create:

1. A constant containing your name.
2. A constant containing your course.
3. A variable containing your current score.
4. Update the score twice.
5. Create a student object and update one property.
6. Explain why the property update is allowed.

---

## Topic 4: Understanding Scope

**Scope** determines where a variable can be accessed in your code.

Understanding scope helps prevent bugs and keeps variables from interfering with unrelated parts of an application.

The three main scope concepts for this session are:

- Global scope
- Function scope
- Block scope

## 4.1 Global Scope

A variable declared at the top level of a script can generally be accessed by functions within that script, subject to module and environment rules.

```js
const instituteName = "Code Academy";

function showInstitute() {
  console.log(instituteName);
}

showInstitute();

console.log(instituteName);
```

Output:

```text
Code Academy
Code Academy
```

The function can access `instituteName` because it is declared in an outer scope.

### When Is This Useful?

A value such as an application configuration setting may need to be available to several functions.

However, avoid making every variable global. Too many global variables can make applications harder to maintain and debug.

## 4.2 Function Scope

A variable declared inside a function is available within that function and its nested scopes, subject to normal declaration rules.

```js
function calculateTotal() {
  const price = 500;
  const quantity = 3;

  const total = price * quantity;

  console.log(total);
}

calculateTotal();
```

Output:

```text
1500
```

The variables `price`, `quantity`, and `total` belong to the function's scope.

Trying to access `price` outside the function produces a `ReferenceError`.

```js
function calculateTotal() {
  const price = 500;
}

calculateTotal();

// console.log(price); // ReferenceError
```

### Why Is Function Scope Useful?

Suppose an application has functions for calculating a product price, student marks, and an order total. Each function can use its own local variables without unnecessarily exposing them to the rest of the program.

## 4.3 Block Scope

A block is a section of code surrounded by curly braces `{}`.

Variables declared with `let` and `const` are block-scoped.

```js
if (true) {
  let message = "Welcome to JavaScript";
  const score = 100;

  console.log(message);
  console.log(score);
}
```

Output:

```text
Welcome to JavaScript
100
```

Outside the block, those variables are unavailable.

```js
if (true) {
  let message = "Hello";
}

// console.log(message); // ReferenceError
```

### Example: Different Blocks

```js
if (true) {
  const status = "Active";
  console.log(status);
}

if (true) {
  const status = "Completed";
  console.log(status);
}
```

Output:

```text
Active
Completed
```

Each block has its own scope, so both declarations are valid.

## 4.4 How `var` Behaves in Blocks

Unlike `let` and `const`, `var` is not block-scoped.

```js
if (true) {
  var oldStyle = "Available outside the block";
  let modernStyle = "Available inside the block";
}

console.log(oldStyle);

// console.log(modernStyle); // ReferenceError
```

Output:

```text
Available outside the block
```

This difference is one reason modern JavaScript code generally favors `let` and `const`.

---

## Topic 5: Scope Shadowing

**Shadowing** occurs when a variable declared in a nested scope has the same name as a variable in an outer scope.

```js
const city = "Anand";

function showCity() {
  const city = "Ahmedabad";

  console.log(city);
}

showCity();

console.log(city);
```

Output:

```text
Ahmedabad
Anand
```

### Explanation

- The outer `city` variable contains `"Anand"`.
- The function declares a separate local `city`.
- Inside the function, the local variable takes precedence.
- Outside the function, the outer variable remains unchanged.

### Block Shadowing

```js
let marks = 70;

if (true) {
  let marks = 90;
  console.log(marks);
}

console.log(marks);
```

Output:

```text
90
70
```

The inner `marks` variable does not modify the outer variable.

### Why Does Shadowing Matter?

Shadowing can be useful when a local variable needs a meaningful name, but excessive reuse of names can confuse readers. Choose variable names that make their purpose clear.

---

## Topic 6: Common Scope Mistakes

### Mistake 1: Accessing a Local Variable Outside Its Function

```js
function greet() {
  const message = "Hello";
}

greet();

console.log(message);
```

This produces a `ReferenceError` because `message` exists only inside `greet()`.

### Mistake 2: Assuming `const` Means the Value Can Never Change

```js
const user = {
  name: "Rahul"
};

user.name = "Amit";

console.log(user.name);
```

Output:

```text
Amit
```

The object property changes, but the variable binding is not reassigned.

### Mistake 3: Declaring Everything Globally

```js
let price;
let quantity;
let total;

function calculate() {
  price = 100;
  quantity = 2;
  total = price * quantity;
}
```

This design unnecessarily places the variables in a wider scope.

A better version is:

```js
function calculate() {
  const price = 100;
  const quantity = 2;
  const total = price * quantity;

  return total;
}

console.log(calculate());
```

Output:

```text
200
```

The improved version keeps the values local and returns the result.

---

# Day 1.1 — End-of-Session Tasks

## Task 1: Student Profile

Create a program containing:

- Student name
- Age
- City
- Course
- Completed task count

Print a formatted student profile.

## Task 2: Scope Demonstration

Create one example each for:

1. Global scope
2. Function scope
3. Block scope
4. Variable shadowing

Add a comment explaining each example.

## Task 3: Shopping Bill

Create a function named `calculateBill()` that:

- Stores the product price.
- Stores the quantity.
- Calculates the total.
- Returns the total.
- Does not expose unnecessary variables globally.

## Task 4: Debugging

Find and fix the errors:

```js
function showStudent() {
  const name = "Asha";
  let marks = 80;
}

showStudent();

console.log(name);
console.log(marks);
```

Explain why the original program fails.

---

# Day 1.1 — Review Questions

1. What is a variable?
2. What is the difference between `let` and `const`?
3. Why should `var` generally be avoided in modern application code?
4. What is global scope?
5. What is function scope?
6. What is block scope?
7. Why does `let` behave differently from `var` inside an `if` block?
8. What is variable shadowing?
9. Does `const` make an object immutable?
10. Why is keeping variables in a smaller scope useful?

## Completion Criteria

Before moving to Day 1.2, make sure you can explain each example in your own words and write a scope-related example without copying from these notes.
