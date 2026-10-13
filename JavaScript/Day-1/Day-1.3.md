# Day 1.3 — Functions and Student Result Processor

## 1. Learning Objectives

By the end of this session, you should be able to:

- Explain why functions are useful.
- Use parameters, arguments, and return values.
- Write function declarations, function expressions, and arrow functions.
- Understand the difference between returning and printing a value.
- Use functions to process arrays of objects.
- Build a Student Result Processor.
- Test your code with normal and edge-case inputs.

## 2. Topics Covered

1. Introduction to reusable functions
2. Parameters and arguments
3. The `return` statement
4. Function declarations
5. Function expressions
6. Arrow functions
7. Function scope and local variables
8. Basic input validation
9. Student Result Processor project

---

## Topic 1: Why Do We Need Functions?

A function is a reusable block of code that performs a particular task.

Imagine that your application needs to calculate a total price in several places. Without a function, you might repeat the same calculation multiple times.

### Without a Function

```js
const price1 = 100;
const quantity1 = 2;
const total1 = price1 * quantity1;

const price2 = 250;
const quantity2 = 3;
const total2 = price2 * quantity2;

console.log(total1);
console.log(total2);
```

### With a Function

```js
function calculateTotal(price, quantity) {
  return price * quantity;
}

console.log(calculateTotal(100, 2));
console.log(calculateTotal(250, 3));
```

Output:

```text
200
750
```

The function allows us to reuse the calculation with different inputs.

### Benefits of Functions

- Reduce repeated code.
- Make programs easier to understand.
- Make logic easier to test.
- Separate large problems into smaller tasks.
- Improve maintainability.

These benefits become especially important when building Express APIs, React applications, and database operations.

---

## Topic 2: Parameters and Arguments

Parameters are variable names listed in a function definition. Arguments are the actual values supplied when the function is called.

```js
function greet(name) {
  console.log("Hello, " + name);
}

greet("Asha");
greet("Rahul");
```

Output:

```text
Hello, Asha
Hello, Rahul
```

In this example:

- `name` is a parameter.
- `"Asha"` and `"Rahul"` are arguments.

### Multiple Parameters

```js
function calculateArea(length, width) {
  return length * width;
}

console.log(calculateArea(10, 5));
```

Output:

```text
50
```

The values `10` and `5` are passed to the parameters `length` and `width`.

### Task

Write functions that accept:

1. Two numbers and return their sum.
2. A name and age and return a formatted sentence.
3. A product price and quantity and return the total price.
4. A student's name and marks and return a formatted result.

---

## Topic 3: The `return` Statement

The `return` statement sends a value back to the code that called a function.

```js
function add(a, b) {
  return a + b;
}

const result = add(5, 7);

console.log(result);
```

Output:

```text
12
```

The function calculates `12` and returns it. The calling code stores that returned value in `result`.

### Returning vs Printing

Consider this function:

```js
function add(a, b) {
  console.log(a + b);
}

const result = add(5, 7);

console.log(result);
```

Output:

```text
12
undefined
```

Why?

- The first `console.log()` displays `12`.
- The function does not explicitly return a value.
- A function without an explicit return produces `undefined`.

### Correct Version

```js
function add(a, b) {
  return a + b;
}

const result = add(5, 7);

console.log(result);
```

Output:

```text
12
```

### Important Rule

A function can return a value so that other parts of the program can use it.

For example:

```js
function calculateTotal(price, quantity) {
  return price * quantity;
}

const total = calculateTotal(100, 3);
const totalWithTax = total + total * 0.18;

console.log(totalWithTax);
```

Output:

```text
354
```

The returned value can be used in further calculations.

---

## Topic 4: Function Declarations

A function declaration defines a named function.

```js
function square(number) {
  return number * number;
}

console.log(square(5));
```

Output:

```text
25
```

### Using Conditions in Functions

```js
function isEven(number) {
  if (number % 2 === 0) {
    return true;
  }

  return false;
}

console.log(isEven(4));
console.log(isEven(7));
```

Output:

```text
true
false
```

The `%` operator returns the remainder after division. Even integers have a remainder of zero when divided by two.

A shorter version is:

```js
function isEven(number) {
  return number % 2 === 0;
}
```

### Task

Write these functions:

- `isPositive(number)`
- `getLargest(a, b, c)`
- `getFullName(firstName, lastName)`
- `calculateDiscount(price, percentage)`

Test each function with at least three inputs.

---

## Topic 5: Function Expressions

A function expression creates a function and assigns it to a variable.

```js
const multiply = function (a, b) {
  return a * b;
};

console.log(multiply(4, 5));
```

Output:

```text
20
```

### Why Use Function Expressions?

They allow functions to be treated as values and passed around in JavaScript.

For example:

```js
const calculate = function (a, b) {
  return a + b;
};

console.log(calculate(10, 20));
```

Output:

```text
30
```

A function expression assigned to a `const` variable must be initialized before that variable is used to call the function.

---

## Topic 6: Arrow Functions

Arrow functions provide a shorter syntax for writing functions.

### Regular Function

```js
function square(number) {
  return number * number;
}
```

### Equivalent Arrow Function

```js
const square = (number) => {
  return number * number;
};
```

### Implicit Return

If the arrow function body consists of a single expression, the braces and `return` can be omitted.

```js
const square = number => number * number;

console.log(square(6));
```

Output:

```text
36
```

### Multiple Parameters

```js
const add = (a, b) => a + b;

console.log(add(10, 15));
```

Output:

```text
25
```

### Returning an Object

When returning an object directly from an arrow function, wrap the object in parentheses.

```js
const createStudent = (name, marks) => ({
  name: name,
  marks: marks
});

console.log(createStudent("Asha", 85));
```

Output:

```text
{ name: 'Asha', marks: 85 }
```

The exact formatting of an object in the console may vary by environment.

### Important Difference

Arrow functions do not have their own `this` binding. Regular functions and arrow functions can therefore behave differently when used as object methods or callbacks. You do not need to master that distinction today, but remember that arrow functions are not simply interchangeable with every regular function.

---

## Topic 7: Functions and Scope

Functions can access variables from their surrounding scopes.

```js
const course = "MERN Stack";

function showCourse() {
  const duration = "12 weeks";

  console.log(course);
  console.log(duration);
}

showCourse();
```

Output:

```text
MERN Stack
12 weeks
```

The function can access `course` from the outer scope, while `duration` is local to the function.

### Return a Value Instead of Printing Everything

```js
function calculateTotal(price, quantity) {
  const total = price * quantity;

  return total;
}

const bill = calculateTotal(200, 3);

console.log("Your bill is:", bill);
```

Output:

```text
Your bill is: 600
```

Returning the result keeps the calculation reusable. Different parts of the application can display, store, or further process the returned value.

---

## Topic 8: Basic Input Validation

Functions should handle unexpected inputs appropriately.

Consider:

```js
function calculateDiscount(price, percentage) {
  return price - price * percentage / 100;
}
```

This function calculates a discounted price, but it does not check whether the inputs are valid.

A more defensive version is:

```js
function calculateDiscount(price, percentage) {
  if (
    typeof price !== "number" ||
    typeof percentage !== "number" ||
    !Number.isFinite(price) ||
    !Number.isFinite(percentage) ||
    price < 0 ||
    percentage < 0 ||
    percentage > 100
  ) {
    return null;
  }

  return price - (price * percentage) / 100;
}

console.log(calculateDiscount(1000, 10)); // 900
console.log(calculateDiscount(1000, 120)); // null
```

Here, `null` represents an invalid calculation. In a real application, you should choose and document an appropriate error-handling strategy.

---

# Practical Project: Student Result Processor

## Project Objective

Build a JavaScript program that processes student records and generates a report.

This project combines:

- Variables
- Scope
- Arrays
- Objects
- Functions
- Parameters and arguments
- Return values
- Conditions
- Basic validation

## Step 1: Create the Student Data

```js
const students = [
  { name: "Asha", marks: 82 },
  { name: "Ravi", marks: 67 },
  { name: "Neha", marks: 91 },
  { name: "Imran", marks: 48 },
  { name: "Meera", marks: 74 }
];
```

Each student is represented by an object containing a name and marks.

## Step 2: Calculate Total Marks

Write a function that accepts an array of students and returns the total marks.

```js
function getTotalMarks(studentList) {
  // Your code here
}
```

Expected result:

```text
362
```

Hint: Start with a total of zero, then add each student's marks.

## Step 3: Calculate Average Marks

```js
function getAverageMarks(studentList) {
  // Your code here
}
```

Expected result:

```text
72.4
```

If the array is empty, return `null` to indicate that an average cannot be calculated.

## Step 4: Determine Pass or Fail

A student passes if their marks are at least 50.

```js
function getStudentResult(student) {
  // Your code here
}
```

Expected examples:

```text
Asha: Pass
Imran: Fail
```

## Step 5: Find a Student

```js
function findStudentByName(studentList, name) {
  // Your code here
}
```

Return the matching student object. If no student matches, return `undefined`.

## Step 6: Generate a Report

```js
function printStudentReport(studentList) {
  // Your code here
}
```

Expected format:

```text
Asha | Marks: 82 | Result: Pass
Ravi | Marks: 67 | Result: Pass
Neha | Marks: 91 | Result: Pass
Imran | Marks: 48 | Result: Fail
Meera | Marks: 74 | Result: Pass
```

## Complete Starter Code

```js
const students = [
  { name: "Asha", marks: 82 },
  { name: "Ravi", marks: 67 },
  { name: "Neha", marks: 91 },
  { name: "Imran", marks: 48 },
  { name: "Meera", marks: 74 }
];

function getTotalMarks(studentList) {
  // TODO: Return total marks.
}

function getAverageMarks(studentList) {
  // TODO: Return the average or null for an empty array.
}

function getStudentResult(student) {
  // TODO: Return Pass or Fail.
}

function findStudentByName(studentList, name) {
  // TODO: Return a student or undefined.
}

function printStudentReport(studentList) {
  // TODO: Print each student's report.
}

printStudentReport(students);

console.log("Total:", getTotalMarks(students));
console.log("Average:", getAverageMarks(students));
console.log("Find Ravi:", findStudentByName(students, "Ravi"));
```

## Project Rules

1. Use functions for each separate operation.
2. Return calculated values rather than only printing them.
3. Keep temporary variables inside the functions that need them.
4. Do not change the original array when calculating totals and averages.
5. Test valid and invalid inputs.
6. Use meaningful variable and function names.

## Stretch Challenges

1. Find the student with the highest marks.
2. Return a new array containing only passing students.
3. Calculate how many students passed.
4. Calculate how many students failed.
5. Create a function that returns a student's grade.
6. Explain what happens if one student's marks are missing.
7. Explain how your functions behave when given an empty array.

---

# Day 1.3 — End-of-Session Tasks

## Task 1: Function Practice

Implement the following functions:

- `isEven(number)`
- `getFullName(firstName, lastName)`
- `calculateDiscount(price, percentage)`
- `getLargest(a, b, c)`
- `formatStudent(student)`

## Task 2: Function Comparison

Implement `calculateTotal()` using:

1. A function declaration.
2. A function expression.
3. An arrow function.

Explain the syntax differences.

## Task 3: Student Result Processor

Complete all five required project functions and test their output.

## Task 4: Explain Your Code

Be prepared to explain:

- Why each function exists.
- Which arguments are passed to it.
- What it returns.
- Which variables are local.
- What happens when invalid inputs are supplied.

---

# Day 1.3 — Review Questions

1. What is a function?
2. What is the difference between a parameter and an argument?
3. What does `return` do?
4. What happens if a function has no explicit return statement?
5. What is the difference between printing and returning a value?
6. What is a function declaration?
7. What is a function expression?
8. What is an arrow function?
9. Why are functions useful in large applications?
10. Why should functions validate inputs when necessary?
11. How can a function return a value that another function uses?
12. Why should a calculation function avoid changing the original input unnecessarily?

