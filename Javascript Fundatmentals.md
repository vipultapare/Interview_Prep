
# JavaScript Variables: `var`, `let`, and `const`

## What is a variable?

A variable is a named container that allows us to store data in our program and use that data later.

```javascript
let name = "Vipul";
let age = 25;

console.log(name);
console.log(age);
```

Here:

- `name` is a variable storing `"Vipul"`.
- `age` is a variable storing `25`.

JavaScript provides three ways to declare variables:

- `var`
- `let`
- `const`

Although all three are used to declare variables, they behave differently.

---

## A. `var`

`var` is the older way of declaring variables in JavaScript.

```javascript
var name = "Vipul";

var name = "Rahul";

console.log(name); // Rahul
```

### What happened?

We declared `name` twice using `var` in the same scope. JavaScript allows this.

### Characteristics of `var`

| Feature | `var` |
|---|---|
| Can be redeclared | Yes |
| Can be reassigned | Yes |
| Function-scoped | Yes |
| Block-scoped | No |
| Hoisted | Yes |

### Example: Redeclaration

```javascript
var x = 10;
var x = 20;

console.log(x); // 20
```

### Example: Reassignment

```javascript
var x = 10;

x = 30;

console.log(x); // 30
```

### Example: `var` ignores block scope

```javascript
if (true) {
    var x = 100;
}

console.log(x); // 100
```

### Why does this happen?

Because `var` is not block-scoped. It is function-scoped or globally scoped, depending on where it is declared.

The `if` block does not create a separate scope for `var`.

---

## B. `let`

`let` was introduced in ES6 (2015) to provide better variable handling.

```javascript
let age = 25;

age = 26;

console.log(age); // 26
```

`let` allows reassignment but does not allow redeclaration in the same scope.

### Characteristics of `let`

| Feature | `let` |
|---|---|
| Can be redeclared in the same scope | No |
| Can be reassigned | Yes |
| Function-scoped | No |
| Block-scoped | Yes |
| Hoisted | Yes |

### Example: Reassignment

```javascript
let age = 25;

age = 30;

console.log(age); // 30
```

### Example: Redeclaration error

```javascript
let age = 25;
let age = 30; // SyntaxError
```

### Why does this fail?

Because `let` cannot be declared twice in the same scope.

However, declaring the same variable in a different scope is allowed.

```javascript
let age = 25;

{
    let age = 30;
    console.log(age); // 30
}

console.log(age); // 25
```

The inner `age` and outer `age` are separate variables.

---

## C. `const`

`const` is used to declare variables whose bindings cannot be reassigned.

```javascript
const age = 25;

console.log(age);
```

### Characteristics of `const`

| Feature | `const` |
|---|---|
| Can be redeclared in the same scope | No |
| Can be reassigned | No |
| Function-scoped | No |
| Block-scoped | Yes |
| Hoisted | Yes |

### Example: Reassignment

```javascript
const age = 25;

age = 30; // TypeError
```

This is not allowed because the variable binding created by `const` cannot be reassigned.

### Example: `const` requires initialization

```javascript
const age; // SyntaxError
```

A `const` declaration must be initialized when it is declared.

### Important: `const` does not make objects immutable

This is one of the most frequently asked JavaScript interview questions.

```javascript
const user = {
    name: "Vipul",
    age: 25
};

user.age = 26;

console.log(user); // { name: "Vipul", age: 26 }
```

This works!

But:

```javascript
const user = {
    name: "Vipul"
};

user = { name: "Rahul" }; // TypeError
```

### Why?

Because `const` prevents reassignment of the variable binding, not modification of the object that the variable references.

Remember this:

- `const` prevents reassignment of the binding.
- It does not freeze the object.
- Object properties can still be modified unless the object is explicitly made immutable.

---

## `var` vs `let` vs `const`

| Feature | `var` | `let` | `const` |
|---|---|---|---|
| Redeclaration | Yes | No (same scope) | No (same scope) |
| Reassignment | Yes | Yes | No |
| Scope | Function | Block | Block |
| Hoisted | Yes | Yes | Yes |
| Temporal Dead Zone (TDZ) | No | Yes | Yes |
| Initialization required | No | No | Yes |

---

## Quick Revision

- `var` allows redeclaration and reassignment.
- `var` is function-scoped, not block-scoped.
- `let` allows reassignment but not redeclaration in the same scope.
- `let` is block-scoped.
- `const` does not allow reassignment or redeclaration in the same scope.
- `const` is block-scoped.
- `const` must be initialized at the time of declaration.
- `const` does not make objects or arrays immutable.
- Prefer `const` by default, and use `let` when reassignment is required.
- Avoid using `var` in modern JavaScript code.


# 2. Data Types: Primitive and Reference Types

## What are Data Types?

JavaScript is a dynamically typed language.

This means we don't need to explicitly declare the type of a variable. JavaScript determines the type based on the value assigned to it.

```javascript
let value = 10;

value = "Hello";

value = true;
```

The same variable can store a number, string, or boolean at different times.

---

## A. Primitive Data Types

Primitive data types represent individual values.

JavaScript has 7 primitive types:

| Type | Example |
|---|---|
| String | `"Hello"` |
| Number | `10`, `3.14` |
| Boolean | `true`, `false` |
| Undefined | `undefined` |
| Null | `null` |
| BigInt | `123n` |
| Symbol | `Symbol("id")` |

### 1. String

Used to represent text.

```javascript
let name = "Vipul";
let city = 'Bangalore';
let message = `Hello ${name}`;
```

JavaScript supports three ways of writing strings:

- Double quotes: `"Hello"`
- Single quotes: `'Hello'`
- Template literals: `` `Hello ${name}` ``

Template literals allow us to embed variables and expressions inside a string using `${}`.

### 2. Number

JavaScript uses the `Number` type for both integers and floating-point numbers, except for values outside the supported precision range and certain specialized cases.

```javascript
let age = 25;
let price = 99.50;
let result = 10 / 3;
```

Examples of Number values:

- Integers: `10`, `25`, `100`
- Floating-point numbers: `3.14`, `99.50`
- Special values: `NaN`, `Infinity`, `-Infinity`

### 3. Boolean

Represents logical values.

A Boolean has only two possible values:

- `true`
- `false`

```javascript
let isLoggedIn = true;
let isAdmin = false;
```

Booleans are commonly used in conditions and decision-making.

### 4. Undefined

A variable that has been declared but not assigned a value has the value `undefined`.

```javascript
let name;

console.log(name); // undefined
```

Here, the variable `name` exists, but we haven't assigned any value to it.

### 5. Null

`null` represents an intentionally absent value.

```javascript
let user = null;
```

Here, we are explicitly assigning `null` to indicate that the variable currently has no user value.

### 6. BigInt

`BigInt` is used to represent integers larger than the safe integer range supported by the `Number` type.

```javascript
let largeNumber = 12345678901234567890n;

console.log(largeNumber);
console.log(typeof largeNumber); // bigint
```

The `n` suffix indicates that the value is a BigInt.

### 7. Symbol

`Symbol` is used to create unique identifiers.

```javascript
const id1 = Symbol("id");
const id2 = Symbol("id");

console.log(id1 === id2); // false
```

Even though both symbols use the same description, they are different symbols.

Each Symbol value is unique.

---

## B. Reference Types

Reference types are values such as objects, arrays and functions.

```javascript
const user = {
    name: "Vipul",
    age: 25
};

const numbers = [10, 20, 30];

function greet() {
    console.log("Hello");
}
```

Common reference-type examples:

- Object
- Array
- Function

### What is the difference between Primitive and Reference Values?

A useful conceptual difference is how values behave when assigned to another variable.

---

### 1. Primitive Example

```javascript
let a = 10;

let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

### What happened?

When `b = a` happens, `b` receives its own primitive value.

Initially:

- `a` contains `10`.
- `b` receives a copy of `10`.

When we change `b` to `20`, it doesn't affect `a`.

Both variables have independent values.

---

### 2. Reference Example

```javascript
const a = {
    name: "Vipul"
};

const b = a;

b.name = "Rahul";

console.log(a.name); // Rahul
console.log(b.name); // Rahul
```

### Why?

Because `a` and `b` refer to the same object.

When we execute:

```javascript
const b = a;
```

Both variables refer to the same object in memory.

When we modify the object's `name` property through `b`, the modification is also visible when accessing the object through `a`.

### Conceptual Illustration

#### Primitive Values

```text
a ----> 10

b ----> 10
```

Both variables hold independent primitive values.

Reassigning `b` doesn't change `a`.

#### Reference Values

```text
a ----\
       \
        ---> Object
       /     name: "Vipul"
b ----/
```

Both variables refer to the same object.

Therefore, modifying the object through one variable affects what we see through the other.

---

## Interview Question: Is an Array a Primitive or Reference Type?

### Answer:

> An array is a reference type in JavaScript. Arrays are objects, and when we assign an array to another variable, both variables can reference the same underlying array. Therefore, modifying the array through one variable can affect the other.

Example:

```javascript
const arr1 = [10, 20, 30];

const arr2 = arr1;

arr2.push(40);

console.log(arr1); // [10, 20, 30, 40]
console.log(arr2); // [10, 20, 30, 40]
```

Both variables refer to the same array.

---

## C. `typeof` Operator

The `typeof` operator is used to determine the type of a value.

```javascript
typeof "Hello";      // "string"
typeof 10;           // "number"
typeof true;         // "boolean"
typeof undefined;    // "undefined"
typeof 10n;          // "bigint"
typeof Symbol();     // "symbol"
typeof {};            // "object"
typeof [];            // "object"
typeof function() {}; // "function"
typeof null;          // "object"
```

### Understanding the `typeof` Results

| Value | `typeof` Result |
|---|---|
| `"Hello"` | `"string"` |
| `10` | `"number"` |
| `true` | `"boolean"` |
| `undefined` | `"undefined"` |
| `10n` | `"bigint"` |
| `Symbol()` | `"symbol"` |
| `{}` | `"object"` |
| `[]` | `"object"` |
| `function() {}` | `"function"` |
| `null` | `"object"` |

### Important Interview Trap: `typeof null`

```javascript
typeof null; // "object"
```

This is a historical JavaScript quirk.

`null` is not actually an object. It is a primitive value.

However, JavaScript returns `"object"` when we use `typeof null`.

To check whether a value is `null`, use:

```javascript
let value = null;

console.log(value === null); // true
```

---

## Quick Revision

- JavaScript is dynamically typed.
- A variable can store values of different data types at different times.
- JavaScript has 7 primitive types: String, Number, Boolean, Undefined, Null, BigInt and Symbol.
- Primitive values are immutable values.
- Objects, arrays and functions are reference types.
- Arrays are objects in JavaScript.
- Primitive assignments result in independent values.
- Object assignments copy the reference, so both variables can refer to the same object.
- `typeof []` returns `"object"`.
- `typeof null` returns `"object"` because of a historical JavaScript quirk.
- Use `=== null` to check whether a value is `null`.

---

## Interview Questions

### 1. How many primitive data types are there in JavaScript?

JavaScript has 7 primitive types:

`String`, `Number`, `Boolean`, `Undefined`, `Null`, `BigInt` and `Symbol`.

### 2. Is JavaScript statically typed or dynamically typed?

JavaScript is dynamically typed. We don't need to explicitly declare the type of a variable, and the same variable can hold values of different types at different times.

### 3. Is an array a primitive data type?

No. An array is an object and is considered a reference type.

### 4. What is the difference between primitive and reference types?

Primitive values behave as independent values when assigned. Objects, arrays and other reference values can be shared through references, meaning multiple variables can access the same underlying object.

### 5. Why does `typeof null` return `"object"`?

It is a historical JavaScript behavior. Although `null` is a primitive value, the `typeof` operator returns `"object"` for it.

### 6. What does `typeof []` return?

```javascript
typeof []; // "object"
```

Arrays are objects in JavaScript.

### 7. What does `typeof function() {}` return?

```javascript
typeof function() {}; // "function"
```

Functions are callable objects, but `typeof` specifically identifies them using `"function"`.



