
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



# 3. Type Coercion

Type coercion is one of the most important JavaScript fundamentals for interviews.

## What is Type Coercion?

Type coercion means JavaScript converts a value from one data type to another data type when performing certain operations.

For example:

```javascript
console.log("5" + 2); // "52"
```

Here, `"5"` is a string and `2` is a number.

JavaScript converts `2` into a string and combines both values.

The result is:

```text
"52" (string)
```

JavaScript performs two kinds of conversions:

- **Implicit coercion** — JavaScript automatically converts the type.
- **Explicit coercion** — We manually convert the type.

---

## A. Implicit Coercion

Implicit coercion happens when JavaScript automatically converts types while evaluating expressions.

### Example 1: String + Number

```javascript
console.log("10" + 5); // "105"
```

### Why?

When `+` is used and one operand is a string, JavaScript often converts the other operand to a string and performs concatenation.

```javascript
"10" + 5
```

Conceptually:

```javascript
"10" + "5"
```

Result:

```javascript
"105"
```

### Example 2: String - Number

```javascript
console.log("10" - 5); // 5
```

### Why?

The `-` operator does not perform string concatenation.

JavaScript converts `"10"` into a number.

```javascript
10 - 5
```

Result:

```javascript
5
```

### Example 3: String * Number

```javascript
console.log("10" * 2); // 20
```

JavaScript converts the string into a number before performing multiplication.

Conceptually:

```javascript
10 * 2
```

Result:

```javascript
20
```

### Example 4: String / Number

```javascript
console.log("20" / 2); // 10
```

Again, `"20"` is converted to a number.

Conceptually:

```javascript
20 / 2
```

Result:

```javascript
10
```

### Example 5: Boolean + Number

```javascript
console.log(true + 1);  // 2
console.log(false + 1); // 1
```

When converted to a number:

- `true` becomes `1`.
- `false` becomes `0`.

Conceptually:

```javascript
1 + 1; // 2
0 + 1; // 1
```

---

## B. Why Does `+` Behave Differently?

The `+` operator is special because it can perform two operations:

1. Numeric addition
2. String concatenation

```javascript
10 + 20;    // 30
"10" + 20;  // "1020"
```

When the operands result in string concatenation, JavaScript combines their string representations.

Other arithmetic operators such as `-`, `*`, and `/` generally perform numeric conversion.

### Comparison of Coercion Behaviour

| Expression | Result | Reason |
|---|---|---|
| `"5" + 2 | `"52"` | String concatenation |
| `"5" - 2 | `3` | Numeric conversion |
| `"5" * 2 | `10` | Numeric conversion |
| `"5" / 2 | `2.5` | Numeric conversion |
| `true + 1` | `2` | Boolean converted to number |
| `false + 1` | `1` | Boolean converted to number |

---

## C. Explicit Coercion

Explicit coercion means we intentionally convert a value from one data type to another.

### 1. Convert to String

We can use the `String()` function to convert a value into a string.

```javascript
let value = 100;

let result = String(value);

console.log(result);       // "100"
console.log(typeof result); // "string"
```

### 2. Convert to Number

We can use the `Number()` function to convert a value into a number.

```javascript
let value = "100";

let result = Number(value);

console.log(result);       // 100
console.log(typeof result); // "number"
```

### Additional Number Conversion Examples

```javascript
console.log(Number("100"));       // 100
console.log(Number("10.5"));      // 10.5
console.log(Number("Hello"));     // NaN
console.log(Number(""));          // 0
console.log(Number(null));        // 0
console.log(Number(undefined));   // NaN
```

### 3. Convert to Boolean

We can use `Boolean()` to convert a value into a Boolean.

```javascript
console.log(Boolean(1));        // true
console.log(Boolean(0));        // false
console.log(Boolean("Hello"));   // true
console.log(Boolean(""));        // false
```

### 4. `parseInt()`

`parseInt()` parses an integer from the beginning of a string, stopping when it encounters a character that cannot be part of the number.

```javascript
console.log(parseInt("100px")); // 100
console.log(parseInt("25.50")); // 25
console.log(parseInt("Hello")); // NaN
```

### 5. `parseFloat()`

`parseFloat()` parses a floating-point number from the beginning of a string.

```javascript
console.log(parseFloat("10.50px")); // 10.5
console.log(parseFloat("25.75"));   // 25.75
console.log(parseFloat("Hello"));   // NaN
```

### Difference Between `Number()`, `parseInt()` and `parseFloat()`

| Function | Example | Result |
|---|---|---|
| `Number()` | `Number("100px")` | `NaN` |
| `parseInt()` | `parseInt("100px")` | `100` |
| `parseFloat()` | `parseFloat("10.50px")` | `10.5` |

---

## D. Common Coercion Interview Traps

```javascript
console.log("5" + 1);       // "51"
console.log("5" - 1);        // 4
console.log("5" * 2);        // 10
console.log("5" / 2);        // 2.5
console.log(5 + true);        // 6
console.log(5 + false);       // 5
console.log(null + 1);        // 1
console.log(undefined + 1);   // NaN
```

### Why does `null + 1` result in `1`?

In numeric operations, `null` converts to `0`.

```javascript
Number(null); // 0
```

Therefore:

```javascript
null + 1
```

Conceptually becomes:

```javascript
0 + 1
```

Result:

```javascript
1
```

### Why does `undefined + 1` result in `NaN`?

```javascript
Number(undefined); // NaN
```

Therefore:

```javascript
undefined + 1
```

JavaScript attempts to perform a numeric operation with `NaN`.

Result:

```javascript
NaN
```

---

## E. Common Type Coercion Conversion Rules

| Value | Numeric Conversion (`Number()`) |
|---|---|
| `true` | `1` |
| `false` | `0` |
| `null` | `0` |
| `undefined` | `NaN` |
| `""` | `0` |
| `"10"` | `10` |
| `"10.5"` | `10.5` |
| `"Hello"` | `NaN` |

### Boolean Conversion

| Value | Boolean Conversion |
|---|---|
| `1` | `true` |
| `0` | `false` |
| `"Hello"` | `true` |
| `""` | `false` |
| `null` | `false` |
| `undefined` | `false` |
| `[]` | `true` |
| `{}` | `true` |

---

## F. Important Interview Concept: `NaN`

`NaN` stands for **Not-a-Number**.

It represents an invalid or unrepresentable numeric result.

```javascript
console.log(Number("Hello")); // NaN
console.log(0 / 0);          // NaN
```

Interestingly:

```javascript
console.log(typeof NaN); // "number"
```

Although it means Not-a-Number, `NaN` belongs to the JavaScript `Number` type.

To check whether a value is `NaN`, use:

```javascript
console.log(Number.isNaN(NaN));       // true
console.log(Number.isNaN("Hello"));   // false
console.log(Number.isNaN(10));        // false
```

---

## Quick Revision

- Type coercion means converting one data type into another.
- Implicit coercion happens automatically.
- Explicit coercion happens when we manually convert values.
- The `+` operator can perform numeric addition or string concatenation.
- When `+` combines strings, it generally converts the other operand to a string.
- Operators like `-`, `*` and `/` generally perform numeric conversion.
- `true` converts to `1` in numeric operations.
- `false` converts to `0` in numeric operations.
- `null` converts to `0` in numeric operations.
- `undefined` converts to `NaN` in numeric operations.
- `Number()` converts a value into a number.
- `String()` converts a value into a string.
- `Boolean()` converts a value into a Boolean.
- `parseInt()` parses an integer from the beginning of a string.
- `parseFloat()` parses a floating-point number from the beginning of a string.
- `NaN` belongs to the `Number` type.

---

## Interview Questions

### 1. What is Type Coercion in JavaScript?

Type coercion is the process of converting a value from one data type to another. JavaScript can perform this conversion automatically or we can perform it manually.

### 2. What is the difference between implicit and explicit coercion?

- Implicit coercion is performed automatically by JavaScript.
- Explicit coercion is performed intentionally by the developer using functions such as `Number()`, `String()` or `Boolean()`.

### 3. Why does `"5" + 2` return `"52"`?

Because the `+` operator performs string concatenation when string conversion is applicable. The number `2` is converted to a string, and both strings are concatenated.

### 4. Why does `"5" - 2` return `3`?

Because the `-` operator performs numeric conversion. The string `"5"` is converted into the number `5`.

### 5. What is the difference between `Number()` and `parseInt()`?

`Number()` attempts to convert the entire value into a number, while `parseInt()` parses an integer from the beginning of a string and stops when it encounters an invalid character.

```javascript
Number("100px");   // NaN
parseInt("100px"); // 100
```

### 6. What is `NaN`?

`NaN` stands for Not-a-Number. It represents an invalid numeric result, but its type is still `number`.

```javascript
typeof NaN; // "number"
```

### 7. Why does `null + 1` return `1`?

Because `null` converts to `0` during numeric conversion.

### 8. Why does `undefined + 1` return `NaN`?

Because `undefined` converts to `NaN` when converted to a number, and arithmetic involving `NaN` results in `NaN`.

### 9. What happens when you add a Boolean and a number?

JavaScript converts the Boolean into a number.

```javascript
true + 1;  // 2
false + 1; // 1
```

### 10. What is the difference between `parseInt()` and `parseFloat()`?

- `parseInt()` parses an integer.
- `parseFloat()` parses a floating-point number.

```javascript
parseInt("10.50");   // 10
parseFloat("10.50"); // 10.5
```




