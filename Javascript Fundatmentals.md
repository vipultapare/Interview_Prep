
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



# 4. `==` vs `===`

This is one of the most commonly asked JavaScript interview questions.

## What is `==`?

`==` is called the **loose equality operator**.

It compares two values after performing type coercion when necessary.

```javascript
console.log(5 == "5"); // true
```

### Why?

- The left side is a number.
- The right side is a string.
- JavaScript converts the string into a number when comparing these values.
- Both values become `5`.

Therefore, the result is `true`.

Conceptually:

```javascript
5 == "5"
```

JavaScript compares:

```javascript
5 == 5
```

Result:

```javascript
true
```

---

## What is `===`?

`===` is called the **strict equality operator**.

It compares both the value and the type without performing the ordinary type coercion associated with `==`.

```javascript
console.log(5 === "5"); // false
```

### Why?

- The left side is a number.
- The right side is a string.
- The types are different.

Therefore, the result is `false`.

---

## A. Comparison Between `==` and `===`

| Feature | `==` | `===` |
|---|---|---|
| Name | Loose equality | Strict equality |
| Compares values | Yes | Yes |
| Compares types strictly | No | Yes |
| Type coercion | Can perform coercion | No ordinary type coercion |
| Predictability | Can produce unexpected results | More predictable |

---

## B. Examples

### Example 1: Number and String

```javascript
console.log(10 == "10");  // true
console.log(10 === "10"); // false
```

With `==`, JavaScript performs type coercion.

With `===`, the types are different, so the comparison returns `false`.

### Example 2: Boolean and Number

```javascript
console.log(true == 1);   // true
console.log(true === 1);  // false
```

With loose equality:

- `true` is converted to `1`.
- `1 == 1` results in `true`.

With strict equality:

- `true` is a Boolean.
- `1` is a Number.
- The types are different.

Therefore, `true === 1` returns `false`.

### Example 3: `null` and `undefined`

```javascript
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

With loose equality, `null` and `undefined` are considered equal to each other.

However, with strict equality, they are different types.

- `null` is a value representing an intentional absence of value.
- `undefined` represents an undefined or unassigned value.

### Example 4: Number and Boolean

```javascript
console.log(0 == false);   // true
console.log(0 === false);  // false
```

With loose equality:

- `false` converts to `0`.
- `0 == 0` results in `true`.

With strict equality:

- `0` is a Number.
- `false` is a Boolean.

Therefore, the result is `false`.

---

## C. What About Objects?

When comparing objects, JavaScript compares their references, not their contents.

```javascript
console.log({} === {}); // false
```

### Why?

Because these are two different object instances.

Even though their contents look the same, they are different objects.

```javascript
const a = {};
const b = {};

console.log(a === b); // false
```

Both objects are created independently.

Therefore, they have different references.

### But what if both variables refer to the same object?

```javascript
const a = {};
const b = a;

console.log(a === b); // true
```

Both variables refer to the same object.

Therefore, the comparison returns `true`.

### Another Example: Arrays

```javascript
const arr1 = [1, 2, 3];
const arr2 = [1, 2, 3];

console.log(arr1 === arr2); // false
```

Even though both arrays contain the same values, they are two different array objects.

But:

```javascript
const arr1 = [1, 2, 3];
const arr2 = arr1;

console.log(arr1 === arr2); // true
```

Both variables refer to the same array.

---

## D. Why Should We Prefer `===`?

We should generally prefer `===` because it avoids unexpected type conversion.

For example:

```javascript
let userId = "5";

if (userId === 5) {
    console.log("Valid");
} else {
    console.log("Invalid");
}
```

Output:

```text
Invalid
```

Why?

- `userId` contains the string `"5"`.
- `5` is a Number.
- Strict equality does not perform ordinary type coercion.

Therefore, the condition evaluates to `false`.

If we used `==`:

```javascript
let userId = "5";

if (userId == 5) {
    console.log("Valid");
}
```

Output:

```text
Valid
```

Because JavaScript converts the string `"5"` into a number during the comparison.

Using strict equality makes code behavior more predictable.

In modern JavaScript, use `===` and `!==` by default.

---

## E. Common Interview Traps

```javascript
console.log(5 == "5");            // true
console.log(5 === "5");           // false

console.log(true == 1);            // true
console.log(true === 1);           // false

console.log(false == 0);           // true
console.log(false === 0);          // false

console.log(null == undefined);    // true
console.log(null === undefined);   // false

console.log(0 == false);           // true
console.log(0 === false);          // false

console.log("" == 0);              // true
console.log("" === 0);             // false

console.log([] == 0);              // true
console.log([] === 0);             // false

console.log([] == []);             // false
console.log({} == {});             // false
```

### Why does `[] == 0` return `true`?

During loose equality comparison, the array is converted to a primitive value.

An empty array converts to an empty string:

```javascript
[].toString(); // ""
```

Then the empty string is converted to a number during the comparison:

```javascript
Number(""); // 0
```

Conceptually:

```javascript
[] == 0
```

Becomes:

```javascript
"" == 0
```

Then:

```javascript
0 == 0
```

Result:

```javascript
true
```

---

## F. Quick Revision

- `==` is the loose equality operator.
- `===` is the strict equality operator.
- `==` can perform type coercion before comparing values.
- `===` does not perform ordinary type coercion.
- `5 == "5"` returns `true`.
- `5 === "5"` returns `false`.
- `true == 1` returns `true`.
- `true === 1` returns `false`.
- `null == undefined` returns `true`.
- `null === undefined` returns `false`.
- Objects and arrays are compared by reference, not by their contents.
- Two different objects with identical properties are not equal.
- Two variables referencing the same object are equal.
- Prefer `===` and `!==` in modern JavaScript.

---

## Interview Questions

### 1. What is the difference between `==` and `===`?

`==` is the loose equality operator. It compares values and may perform type coercion before comparison.

`===` is the strict equality operator. It compares values without ordinary type coercion and considers different types unequal.

### 2. Why does `5 == "5"` return `true`?

Because loose equality performs type coercion. JavaScript converts the string `"5"` into the number `5` before comparison.

### 3. Why does `5 === "5"` return `false`?

Because one value is a Number and the other is a String. Strict equality does not perform ordinary type coercion.

### 4. Why does `null == undefined` return `true`?

The loose equality algorithm specifically considers `null` and `undefined` equal to each other.

### 5. Why does `[] === []` return `false`?

Because each array expression creates a different object. JavaScript compares object references, not their contents.

### 6. Why does `{} === {}` return `false`?

Because both object literals create separate objects with different references.

### 7. Why should we use `===` instead of `==`?

Strict equality avoids unexpected type coercion and makes comparisons more predictable. This is why it is generally preferred in modern JavaScript.

### 8. What is the difference between value comparison and reference comparison?

- Primitive values are compared based on their values.
- Objects and arrays are compared based on whether they refer to the same object.

### 9. Is `==` always bad?

No. It is not inherently bad, but it can produce surprising results due to coercion. It can be used intentionally when its coercion behavior is understood. However, `===` is generally the preferred default.



# 5. `null` vs `undefined`

These two values look similar, but their meaning is different.

## What is `undefined`?

`undefined` generally means a value has not been assigned or is unavailable.

```javascript
let name;

console.log(name); // undefined
```

Here, we declared the variable but did not assign a value.

### Other Examples of `undefined`

#### 1. A variable without an assigned value

```javascript
let age;

console.log(age); // undefined
```

The variable is declared, but no value is assigned to it.

#### 2. A function without a return statement

```javascript
function greet() {
    console.log("Hello");
}

const result = greet();

console.log(result); // undefined
```

The function executes, but it does not explicitly return a value.

In JavaScript, a function that doesn't return a value explicitly returns `undefined`.

#### 3. Missing object property

```javascript
const user = {
    name: "Vipul"
};

console.log(user.age); // undefined
```

The property `age` doesn't exist on the object.

When we access a missing object property, JavaScript returns `undefined`.

#### 4. Missing function argument

```javascript
function greet(name) {
    console.log(name);
}

greet(); // undefined
```

The parameter `name` receives `undefined` because no argument was provided.

---

## A. What is `null`?

`null` represents an intentionally empty or absent value.

```javascript
let user = null;
```

Here, we explicitly assign `null` to indicate that the variable currently has no user object.

### Example

```javascript
let selectedUser = null;

// Later:
selectedUser = {
    name: "Vipul"
};

console.log(selectedUser); // { name: "Vipul" }
```

Initially, there is no selected user.

Later, a user is assigned.

### Another Example

```javascript
const user = {
    name: "Vipul",
    profile: null
};
```

Here, the `profile` property exists, but its value is intentionally set to `null`.

This can indicate that the profile information is currently absent.

---

## B. Difference Between `null` and `undefined`

| Feature | `undefined` | `null` |
|---|---|---|
| Meaning | Value has not been assigned or is unavailable | Intentional absence of a value |
| Assignment | Often assigned automatically by JavaScript | Usually assigned intentionally |
| `typeof` result | `"undefined"` | `"object"` |
| Missing object property | Can result in `undefined` | Not automatically returned for missing properties |
| Typical usage | Indicates an uninitialized or unavailable value | Indicates an intentionally empty value |

---

## C. Interview Example

```javascript
let a;
let b = null;

console.log(a); // undefined
console.log(b); // null
```

### What is the difference?

- `a`: I haven't assigned a value.
- `b`: I intentionally assigned an empty value.

The difference is primarily the intention behind the value.

---

## D. Important: `null` vs `undefined` with Equality

```javascript
console.log(null == undefined);  // true
console.log(null === undefined); // false
```

### Why?

With loose equality (`==`), JavaScript considers `null` and `undefined` equal to each other.

With strict equality (`===`), they are not equal because they are different types.

```javascript
typeof null;      // "object"
typeof undefined; // "undefined"
```

---

## E. Common Interview Traps

```javascript
console.log(null == undefined);   // true
console.log(null === undefined);  // false

console.log(null == 0);          // false
console.log(null === 0);         // false

console.log(undefined == 0);      // false
console.log(undefined === 0);     // false

console.log(null + 1);            // 1
console.log(undefined + 1);        // NaN
```

### Why does `null == 0` return `false`?

Although `null` converts to `0` in numeric operations, loose equality comparison between `null` and other values does not follow the same conversion rules.

`null` is loosely equal to `undefined`, but it is not loosely equal to `0`, `false`, or an empty string.

```javascript
console.log(null == undefined); // true
console.log(null == 0);        // false
console.log(null == false);    // false
console.log(null == "");        // false
```

This is an important JavaScript interview concept.

---

## F. Quick Revision

- `undefined` generally indicates that a value hasn't been assigned or is unavailable.
- `null` represents an intentional absence of a value.
- JavaScript automatically produces `undefined` in many situations.
- `null` is usually assigned intentionally by the developer.
- A declared variable without an assigned value contains `undefined`.
- A missing object property returns `undefined`.
- A function without an explicit return value returns `undefined`.
- A missing function argument results in `undefined` for that parameter.
- `typeof undefined` returns `"undefined"`.
- `typeof null` returns `"object"` due to a historical JavaScript quirk.
- `null == undefined` returns `true`.
- `null === undefined` returns `false`.
- `null` is not loosely equal to `0`, `false`, or `""`.

---

## Interview Questions

### 1. What is the difference between `null` and `undefined`?

`undefined` generally indicates that a value hasn't been assigned or is unavailable. `null` represents an intentional absence of a value.

### 2. When does JavaScript return `undefined`?

JavaScript can return `undefined` in several situations:

- A variable is declared but not initialized.
- An object property does not exist.
- A function doesn't explicitly return a value.
- A function parameter is not provided.

### 3. Why does `typeof null` return `"object"`?

This is a historical JavaScript bug/quirk that has been preserved for backward compatibility. `null` is actually a primitive value, not an object.

### 4. Is `null == undefined` true?

Yes.

```javascript
null == undefined; // true
```

The loose equality algorithm specifically treats these two values as equal.

### 5. Is `null === undefined` true?

No.

```javascript
null === undefined; // false
```

Strict equality considers their types, which are different.

### 6. Is `null` equal to `0`?

No.

```javascript
null == 0; // false
```

Although `null` converts to `0` in numeric operations, loose equality does not make `null` equal to `0`.

### 7. What is the difference between `null + 1` and `undefined + 1`?

```javascript
null + 1;      // 1
undefined + 1;  // NaN
```

In numeric operations:

- `null` converts to `0`.
- `undefined` converts to `NaN`.

Therefore, the results are different.



# JavaScript Scope

## What is Scope?

Scope defines where a variable, function, or object can be accessed within JavaScript code.

In simple words, **scope determines the visibility and accessibility of variables** in our code.

JavaScript commonly involves three types of scope:

- Global Scope
- Function Scope
- Block Scope

---

## 1. Global Scope

A variable declared outside functions and blocks at the top level is in the global scope.

It can generally be accessed throughout the applicable global scope.

### Example

```javascript
const company = "OpenAI";

function showCompany() {
    console.log(company);
}

showCompany();
console.log(company);
```

### Output

```text
OpenAI
OpenAI
```

### Explanation

- `company` is declared outside the function.
- It belongs to the global scope in this script.
- It can be accessed inside `showCompany()`.
- It can also be accessed outside the function.

### Interview Answer

Global scope means a variable is declared at the top level, outside functions and blocks, making it accessible throughout the applicable scope of the program.

However, we should avoid creating too many global variables because they can cause naming conflicts and unintended modifications.

---

## 2. Function Scope

Function scope means a variable declared inside a function can only be accessed within that function.

Variables declared using `var`, `let`, and `const` inside a function cannot be directly accessed outside that function.

### Example

```javascript
function login() {
    const username = "Vipul";

    console.log(username);
}

login();

console.log(username);
```

### Output

```text
Vipul
ReferenceError: username is not defined
```

### Explanation

- `username` is declared inside the `login()` function.
- It can be accessed inside the function.
- It cannot be accessed directly outside the function.

### Interview Answer

Function scope means variables declared inside a function are accessible only within that function and its nested scopes.

---

## 3. Block Scope

Block scope means a variable declared inside a block `{}` using `let` or `const` can only be accessed within that block.

Blocks can be created using:

- `if`
- `else`
- `for`
- `while`
- `{}`

### Example Using `let`

```javascript
if (true) {
    let age = 25;

    console.log(age);
}

console.log(age);
```

### Output

```text
25
ReferenceError: age is not defined
```

### Explanation

- `age` is declared inside the `if` block.
- It is accessible inside that block.
- It cannot be accessed outside the block.

### Example Using `const`

```javascript
if (true) {
    const city = "Bangalore";

    console.log(city);
}

console.log(city);
```

### Output

```text
Bangalore
ReferenceError: city is not defined
```

### Interview Answer

Block scope means variables declared using `let` and `const` inside curly braces are accessible only within that block and its nested scopes.

---

## 4. `var` vs `let` vs `const` in Scope

This is one of the most important scope-related interview questions.

### Using `var`

```javascript
if (true) {
    var age = 25;
}

console.log(age);
```

### Output

```text
25
```

### Explanation

`var` is not block-scoped.

It ignores the `if` block boundary and is accessible outside the block, provided it is not enclosed within a function.

---

### Using `let`

```javascript
if (true) {
    let age = 25;
}

console.log(age);
```

### Output

```text
ReferenceError: age is not defined
```

### Explanation

`let` is block-scoped, so it cannot be accessed outside the block in which it was declared.

---

### Using `const`

```javascript
if (true) {
    const age = 25;
}

console.log(age);
```

### Output

```text
ReferenceError: age is not defined
```

### Explanation

`const` is also block-scoped.

---

## 5. Scope Comparison

| Scope | Declaration Location | Accessibility |
|---|---|---|
| Global Scope | Top-level, outside functions and blocks | Throughout the applicable global scope |
| Function Scope | Inside a function | Inside that function and nested scopes |
| Block Scope | Inside `{}` using `let` or `const` | Inside that block and nested scopes |

---

## 6. `var`, `let`, and `const` Comparison

| Variable | Function Scoped | Block Scoped |
|---|---|---|
| `var` | Yes | No |
| `let` | No | Yes |
| `const` | No | Yes |

### Remember

- `var` is function-scoped.
- `let` is block-scoped.
- `const` is block-scoped.

---

## 7. Practical Example Combining All Scopes

```javascript
const company = "ABC";

function employee() {
    let employeeName = "Vipul";

    if (true) {
        const role = "Developer";

        console.log(company);
        console.log(employeeName);
        console.log(role);
    }

    console.log(employeeName);
    console.log(role);
}

employee();

console.log(company);
console.log(employeeName);
```

### Explanation

| Variable | Scope | Accessibility |
|---|---|---|
| `company` | Global | Accessible throughout the applicable scope |
| `employeeName` | Function | Accessible inside the function and its nested scopes |
| `role` | Block | Accessible inside the `if` block and its nested scopes |

### What will happen?

- `company` can be accessed inside the function and outside it.
- `employeeName` can be accessed inside `employee()` but not outside.
- `role` can be accessed inside the `if` block but not outside it.
- `console.log(role)` outside the `if` block throws a `ReferenceError`.
- `console.log(employeeName)` outside the function throws a `ReferenceError`.

---

## 8. Real-Life Analogy

Think about scope like access permissions in an office.

### Global Scope

A notice board accessible to everyone in the office.

### Function Scope

A private meeting room. People outside cannot directly access the information inside.

### Block Scope

A restricted area within the meeting room. Only people inside that area can access its resources.

---

## 9. Interview Revision

### What is Scope?

Scope determines where variables and functions can be accessed in JavaScript.

### What is Global Scope?

Variables declared at the top level can generally be accessed throughout the applicable global scope.

### What is Function Scope?

Variables declared inside a function can only be directly accessed within that function and its nested scopes.

### What is Block Scope?

Variables declared using `let` and `const` inside curly braces can only be accessed within that block and its nested scopes.

### Is `var` block-scoped?

No. `var` is function-scoped, not block-scoped.

### Are `let` and `const` block-scoped?

Yes. Both `let` and `const` are block-scoped.

---

## 10. Important Topics to Study Next

After understanding scope, study these concepts in order:

1. Lexical Scope
2. Scope Chain
3. Variable Shadowing
4. Hoisting
5. Temporal Dead Zone (TDZ)
6. Closures

These concepts are closely related and are frequently asked in JavaScript interviews.


# JavaScript Hoisting

## What is Hoisting?

Hoisting is a JavaScript behavior where declarations are processed before code execution, which affects how variables and functions can be accessed before the line where they are written.

In simple words, **JavaScript prepares certain declarations before executing the code.**

However, hoisting does not mean JavaScript physically moves the code to the top. It is a conceptual way of understanding how JavaScript handles declarations during execution.

---

## 1. Hoisting with `var`

Variables declared using `var` are hoisted and initialized with `undefined`.

### Example

```javascript
console.log(name);

var name = "Vipul";

console.log(name);
```

### Output

```text
undefined
Vipul
```

### Why does this happen?

The declaration of `name` is processed before execution, but the assignment happens when JavaScript reaches that line.

### Conceptual representation

```javascript
var name;

console.log(name); // undefined

name = "Vipul";

console.log(name); // Vipul
```

### Explanation

- The declaration `var name` is processed before execution.
- Initially, the variable contains `undefined`.
- When JavaScript reaches `name = "Vipul"`, the value is assigned.
- The second `console.log()` prints `Vipul`.

### Interview Answer

Variables declared using `var` are hoisted to their function scope or global scope, depending on where they are declared. They are initialized with `undefined`, so accessing them before their assignment returns `undefined`.

---

## 2. Hoisting with `let`

Variables declared using `let` are hoisted, but they are not initialized with a value that allows access before their declaration is executed.

### Example

```javascript
console.log(a);

let a = 10;
```

### Output

```text
ReferenceError: Cannot access 'a' before initialization
```

### Why does this happen?

- The `let` declaration is associated with its scope before execution.
- However, the variable cannot be accessed before its declaration is executed.
- During this period, the variable is in the Temporal Dead Zone (TDZ).

### Example

```javascript
// Temporal Dead Zone starts

console.log(a); // ReferenceError

let a = 10; // TDZ ends for a
```

### Interview Answer

`let` variables are hoisted, but they remain uninitialized until their declaration is executed. Accessing them before that results in a ReferenceError because of the Temporal Dead Zone.

---

## 3. Hoisting with `const`

`const` behaves similarly to `let` regarding hoisting.

### Example

```javascript
console.log(a);

const a = 10;
```

### Output

```text
ReferenceError: Cannot access 'a' before initialization
```

### Why does this happen?

- `const` is hoisted.
- It remains uninitialized until its declaration is executed.
- Accessing it before initialization results in a ReferenceError.
- A `const` declaration must also include an initial value.

### Correct Example

```javascript
const a = 10;

console.log(a); // 10
```

### Interview Answer

`const` variables are hoisted but remain uninitialized during the Temporal Dead Zone. Accessing them before the declaration is executed results in a ReferenceError.

---

## 4. Hoisting with Function Declaration

Function declarations can be called before they appear in the code.

### Example

```javascript
greet();

function greet() {
    console.log("Hello Vipul");
}
```

### Output

```text
Hello Vipul
```

### Why does this happen?

Function declarations are available during execution before their position in the source code.

Therefore, we can call a function before its declaration.

### Example

```javascript
function greet() {
    console.log("Hello Vipul");
}

greet();
```

Both examples produce the same output.

### Interview Answer

Function declarations are hoisted along with their definitions, which means we can call them before they appear in the code.

---

## 5. Hoisting with Function Expression

A function expression behaves differently from a function declaration.

### Example

```javascript
greet();

var greet = function () {
    console.log("Hello");
};
```

### Output

```text
TypeError: greet is not a function
```

### Why does this happen?

- `var greet` is hoisted.
- Initially, `greet` contains `undefined`.
- The function is assigned to `greet` only when execution reaches the assignment.
- When `greet()` executes earlier, JavaScript tries to call `undefined` as a function.

### Conceptual Representation

```javascript
var greet;

greet(); // TypeError

greet = function () {
    console.log("Hello");
};
```

### Interview Answer

In a function expression, the variable declaration is hoisted, but the function assignment is not. Therefore, calling the function before the assignment results in a TypeError when using `var`.

---

## 6. Hoisting with Arrow Functions

Arrow functions also behave like function expressions.

### Example Using `const`

```javascript
hello();

const hello = () => {
    console.log("Hello");
};
```

### Output

```text
ReferenceError: Cannot access 'hello' before initialization
```

### Why does this happen?

- The `const` declaration is hoisted.
- It remains uninitialized until the declaration is executed.
- The function assignment has not happened yet.
- Accessing `hello` before initialization results in a ReferenceError.

### Example Using `var`

```javascript
hello();

var hello = () => {
    console.log("Hello");
};
```

### Output

```text
TypeError: hello is not a function
```

### Why?

Because `hello` is initially `undefined`, and JavaScript cannot call `undefined` as a function.

---

## 7. Function Declaration vs Function Expression

| Feature | Function Declaration | Function Expression |
|---|---|---|
| Example | `function greet() {}` | `const greet = function() {}` |
| Hoisting | Function definition is available | Variable declaration is hoisted |
| Can call before declaration? | Yes | No, not in the typical way |
| Function available before execution reaches the declaration? | Yes | No |

---

## 8. `var` vs `let` vs `const` in Hoisting

| Variable | Hoisted | Initial Value Before Declaration Executes | Access Before Declaration |
|---|---|---|---|
| `var` | Yes | `undefined` | Allowed |
| `let` | Yes | Uninitialized | ReferenceError |
| `const` | Yes | Uninitialized | ReferenceError |

### Remember

- `var` → Hoisted and initialized with `undefined`.
- `let` → Hoisted but uninitialized.
- `const` → Hoisted but uninitialized.
- `let` and `const` → Temporal Dead Zone before initialization.

---

## 9. Tricky Interview Questions

### Question 1

```javascript
console.log(a);

var a = 5;

console.log(a);
```

### Output

```text
undefined
5
```

### Explanation

The `var` declaration is hoisted, but the assignment happens later.

---

### Question 2

```javascript
console.log(a);

let a = 5;
```

### Output

```text
ReferenceError
```

### Explanation

The variable is in the Temporal Dead Zone until its declaration is executed.

---

### Question 3

```javascript
greet();

function greet() {
    console.log("Hello");
}
```

### Output

```text
Hello
```

### Explanation

Function declarations are hoisted along with their definitions.

---

### Question 4

```javascript
greet();

var greet = function () {
    console.log("Hello");
};
```

### Output

```text
TypeError: greet is not a function
```

### Explanation

The variable is hoisted, but its function assignment happens later.

---

### Question 5

```javascript
var a = 10;

function test() {
    console.log(a);

    var a = 20;
}

test();
```

### Output

```text
undefined
```

### Explanation

The local variable `a` inside the function is hoisted to the function scope.

Conceptually, JavaScript behaves like this:

```javascript
var a = 10;

function test() {
    var a;

    console.log(a); // undefined

    a = 20;
}

test();
```

The local `a` shadows the global `a` inside the function.

---

### Question 6

```javascript
var a = 10;

function test() {
    console.log(a);
}

test();
```

### Output

```text
10
```

### Explanation

There is no local variable `a` inside `test()`, so JavaScript looks in the outer scope and finds the global variable.

---

## 10. What is Temporal Dead Zone (TDZ)?

The Temporal Dead Zone is the period between entering a scope and the point where a `let` or `const` declaration is executed.

During this period, the variable exists in its scope but cannot be accessed.

### Example

```javascript
{
    // TDZ starts

    console.log(a); // ReferenceError

    let a = 10; // TDZ ends

    console.log(a); // 10
}
```

### Explanation

- The scope begins.
- The variable `a` is associated with the block but is uninitialized.
- Accessing `a` before its declaration results in a ReferenceError.
- Once the declaration executes, `a` can be accessed.

---

## 11. Real-Life Analogy

Imagine a company preparing for a meeting.

### `var`

The employee's name is already on the list, but the value is initially marked as `undefined`. You can check the list, but the actual information has not been assigned yet.

### `let` and `const`

The employee's record exists, but it is temporarily locked. You cannot access the information until the initialization process is completed.

### Function Declaration

A meeting's agenda and instructions are already available, so you can refer to them before the meeting's position in the schedule.

### Function Expression

The instructions are created and assigned only when that particular step is reached.

---

## 12. How to Explain Hoisting in an Interview

Hoisting is a JavaScript behavior where declarations are processed before code execution, which affects how variables and functions can be accessed before the line where they are written.

For example, variables declared using `var` are hoisted and initialized with `undefined`, so accessing them before their assignment returns `undefined`.

However, `let` and `const` are also hoisted, but they remain uninitialized until their declaration is executed. Accessing them before that results in a ReferenceError due to the Temporal Dead Zone.

Function declarations are hoisted along with their definitions, so we can call them before they appear in our code.

But function expressions and arrow functions behave differently because only the variable declaration is hoisted, not the function assignment.

---

## 13. Quick Revision Notes

| Concept | Remember |
|---|---|
| Hoisting | Declarations are processed before execution |
| `var` | Hoisted and initialized with `undefined` |
| `let` | Hoisted but uninitialized |
| `const` | Hoisted but uninitialized |
| Function declaration | Function definition is available before its code position |
| Function expression | Function assignment happens during execution |
| Arrow function | Behaves like a function expression for hoisting |
| TDZ | Period before `let`/`const` initialization |
| `ReferenceError` | Accessing uninitialized `let`/`const` |
| `TypeError` | Attempting to call a non-function value such as `undefined` |

---

## 14. Topics to Study Next

After understanding Hoisting, study these topics:

1. Temporal Dead Zone (TDZ)
2. Lexical Scope
3. Scope Chain
4. Variable Shadowing
5. Closures
6. Execution Context
7. Call Stack



# JavaScript Closures

## 1. What is a Closure?

A **closure** is a feature in JavaScript where an inner function remembers and can access the variables of its outer function, even after the outer function has finished executing.

### Simple Definition

A closure allows a function to remember the variables that were available in the scope where it was created.

---

## 2. Understanding Closure with a Simple Example

```javascript
function outer() {
  let name = "Vipul";

  function inner() {
    console.log(name);
  }

  inner();
}

outer();
```

### Output

```text
Vipul
```

### Explanation

1. We created an `outer()` function.
2. Inside `outer()`, we declared a variable called `name`.
3. We created another function called `inner()`.
4. The `inner()` function accesses the `name` variable from its outer function.
5. JavaScript allows inner functions to access variables from their outer scope.

This is the basic concept behind closures.

---

## 3. Understanding Closure When the Outer Function Finishes

This is the most important example to understand closures.

```javascript
function outer() {
  let name = "Vipul";

  return function inner() {
    console.log(name);
  };
}

const result = outer();

result();
```

### Output

```text
Vipul
```

### Step-by-Step Explanation

#### Step 1: Call the outer function

```javascript
const result = outer();
```

The `outer()` function executes.

Inside it:

```javascript
let name = "Vipul";
```

The variable `name` is created.

#### Step 2: Return the inner function

```javascript
return function inner() {
  console.log(name);
};
```

Instead of executing the inner function, the outer function returns it.

#### Step 3: Store the returned function

```javascript
const result = outer();
```

Now, `result` contains the returned inner function.

#### Step 4: Execute the inner function

```javascript
result();
```

The inner function executes and prints:

```text
Vipul
```

Even though `outer()` has already finished executing, the inner function still has access to the `name` variable.

**This retained access to the outer variable is the important part of a closure.**

---

## 4. Closure with a Counter Example

Closures are commonly used to maintain state.

```javascript
function counter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const increment = counter();

increment();
increment();
increment();
```

### Output

```text
1
2
3
```

### Step-by-Step Explanation

#### Step 1: Create the counter

```javascript
function counter() {
  let count = 0;
```

We created a variable `count` and initialized it with `0`.

#### Step 2: Return the inner function

```javascript
return function () {
  count++;
  console.log(count);
};
```

The inner function increments `count` and prints its value.

#### Step 3: Call the outer function

```javascript
const increment = counter();
```

The outer function executes once and returns the inner function.

#### Step 4: Call increment

```javascript
increment();
```

The inner function executes.

It increases the `count` value from `0` to `1`.

#### Step 5: Call increment again

```javascript
increment();
```

The same `count` variable is used again.

It increases from `1` to `2`.

#### Step 6: Call increment one more time

```javascript
increment();
```

It increases from `2` to `3`.

### Why does count not reset to 0?

Because the inner function retains access to the same `count` variable from the outer function.

The outer function is not called again every time `increment()` is called.

---

## 5. Closure as a Backpack

Imagine a function carrying a backpack.

The backpack contains the variables that the function can still access from its surrounding environment.

When the outer function finishes executing, the inner function can still access the variables it needs.

```javascript
function outer() {
  let message = "Hello";

  return function () {
    console.log(message);
  };
}

const greet = outer();

greet();
```

The returned function still has access to `message`.

You can think of closure as a function carrying access to its surrounding variables.

---

## 6. Closure for Data Privacy

Closures can help protect variables from being directly accessed outside a function.

```javascript
function bankAccount() {
  let balance = 1000;

  return {
    deposit: function (amount) {
      balance += amount;
    },

    getBalance: function () {
      return balance;
    }
  };
}

const account = bankAccount();

account.deposit(500);

console.log(account.getBalance());
```

### Output

```text
1500
```

### Explanation

The `balance` variable is declared inside `bankAccount()`.

We cannot directly access it like this:

```javascript
console.log(account.balance);
```

It will return:

```text
undefined
```

Instead, we access and modify the balance through the returned methods.

```javascript
account.deposit(500);
account.getBalance();
```

The returned functions retain access to `balance` through closure.

---

## 7. Where Are Closures Used?

Closures are commonly used in JavaScript for:

- Maintaining state inside functions.
- Data privacy.
- Event handlers.
- Callbacks.
- Timers such as `setTimeout`.
- React hooks and functional components.
- Memoization.
- Function factories.

---

## 8. Closure in JavaScript Interview Questions

### Q1. What is a closure?

A closure is a feature in JavaScript where a function retains access to variables from its lexical scope, even after the outer function has finished executing.

### Q2. Why do we use closures?

Closures are used to maintain state, create private variables, implement callbacks and manage data without exposing it directly.

### Q3. Can a closure access outer function variables?

Yes. An inner function can access variables declared in its outer function.

### Q4. Does a closure keep the outer function executing?

No. The outer function finishes executing, but the inner function can retain access to the variables it needs from that outer scope.

### Q5. Give a real example of a closure.

A counter function is a common example. It maintains a count variable and increments it every time the returned function is called.

---

## 9. Interview Example to Practice

```javascript
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment());
console.log(increment());
console.log(increment());
```

### Output

```text
1
2
3
```

### Interview Explanation

The `counter()` function initializes `count` to zero and returns an inner function.

The returned function retains access to the `count` variable through closure. Whenever I call `increment()`, the same variable is incremented instead of being initialized again.

This is an example of how closures help maintain state.

---

## 10. Quick Revision

- A closure is created when a function retains access to its lexical environment.
- Inner functions can access variables from outer functions.
- A closure can continue accessing outer variables after the outer function finishes.
- Closures help maintain state.
- Closures can help implement private variables.
- Closures are commonly used in callbacks, event handlers and React.

### Remember This Example

```javascript
function counter() {
  let count = 0;

  return function () {
    count++;
    console.log(count);
  };
}

const increment = counter();

increment(); // 1
increment(); // 2
increment(); // 3
```

**The inner function remembers the `count` variable. That is the core idea of closure.**



# Lexical Scope in JavaScript

## 1. What is Lexical Scope?

**Lexical scope means JavaScript determines which variables a function can access based on where the function is written (defined), not where the function is called.**

In simple words, the location where you write a function determines which variables it can access.

---

## 2. Simple Example of Lexical Scope

```javascript
const name = "Vipul";

function greet() {
  console.log(name);
}

greet();
```

### Output

```text
Vipul
```

### Explanation

1. We declared a variable called `name` outside the function.
2. We created a function called `greet()`.
3. The `greet()` function can access the `name` variable because it is available in its outer scope.
4. When we call `greet()`, JavaScript prints `Vipul`.

---

## 3. Lexical Scope with Nested Functions

```javascript
function outer() {
  let name = "Vipul";

  function inner() {
    console.log(name);
  }

  inner();
}

outer();
```

### Output

```text
Vipul
```

### Explanation

1. We created an `outer()` function.
2. Inside `outer()`, we declared a variable `name`.
3. We created an `inner()` function inside `outer()`.
4. The `inner()` function tries to access `name`.
5. JavaScript searches inside the `inner()` function first.
6. It does not find `name`.
7. JavaScript then searches in the outer scope.
8. It finds `name = "Vipul"` and prints it.

**An inner function can access variables from its outer function.**

---

## 4. Scope Access Direction

JavaScript allows inner scopes to access variables from outer scopes.

However, outer scopes cannot directly access variables from inner scopes.

### Example

```javascript
function outer() {
  function inner() {
    let message = "Hello";

    console.log(message);
  }

  inner();

  console.log(message);
}

outer();
```

### Output

```text
Hello
ReferenceError: message is not defined
```

### Why?

The `message` variable is declared inside the `inner()` function.

Therefore, it belongs to the scope of `inner()` and cannot be directly accessed by `outer()`.

### Remember

- Inner scope can access outer scope variables.
- Outer scope cannot access inner scope variables.

---

## 5. Lexical Scope vs Dynamic Scope

JavaScript uses lexical scope, not dynamic scope.

### Example

```javascript
let name = "Global";

function outer() {
  let name = "Outer";

  function inner() {
    console.log(name);
  }

  return inner;
}

const result = outer();

function anotherFunction() {
  let name = "Another Function";

  result();
}

anotherFunction();
```

### Output

```text
Outer
```

### Why is the output `Outer`?

1. The `inner()` function is written inside `outer()`.
2. Therefore, `inner()` is lexically connected to the scope of `outer()`.
3. When `inner()` searches for `name`, it finds `name` in `outer()`.
4. It prints `Outer`.

Even though `result()` is called from inside `anotherFunction()`, it does not use the scope of `anotherFunction()` to resolve the variable.

**JavaScript determines variable access based on where the function is defined, not where it is called.**

---

## 6. What is the Scope Chain?

When JavaScript needs a variable, it searches for that variable in the following order:

1. Current scope.
2. Parent scope.
3. Further outer scopes.
4. Global scope.

If the variable is not found anywhere, JavaScript throws a `ReferenceError` (when trying to access an undeclared identifier).

### Example

```javascript
let globalVariable = "Global";

function outer() {
  let outerVariable = "Outer";

  function inner() {
    let innerVariable = "Inner";

    console.log(innerVariable);
    console.log(outerVariable);
    console.log(globalVariable);
  }

  inner();
}

outer();
```

### Output

```text
Inner
Outer
Global
```

### How does JavaScript search?

When `inner()` executes:

- `innerVariable` is found in the inner scope.
- `outerVariable` is found in the outer scope.
- `globalVariable` is found in the global scope.

This lookup mechanism is called the **Scope Chain**.

---

## 7. Lexical Scope and Closures

Lexical scope is the foundation of closures.

### Example

```javascript
function outer() {
  let name = "Vipul";

  return function inner() {
    console.log(name);
  };
}

const result = outer();

result();
```

### Output

```text
Vipul
```

### Explanation

1. `outer()` executes.
2. It creates the `name` variable.
3. It returns the `inner()` function.
4. The outer function finishes executing.
5. We call the returned function.
6. The inner function still has access to `name`.

This is an example of a closure.

### Difference

| Lexical Scope | Closure |
|---|---|
| Determines variable access based on where code is written. | A function retains access to variables from its surrounding lexical environment. |
| Defines how variable lookup works. | Allows access to surrounding variables even after the outer function finishes. |
| It is the foundation of closures. | It uses lexical scope to retain access to variables. |

---

## 8. Interview Questions

### Q1. What is lexical scope?

Lexical scope means that variable accessibility is determined by where a function or block is defined in the source code, rather than where it is called.

### Q2. Does JavaScript use lexical scope or dynamic scope?

JavaScript uses lexical scope.

### Q3. Can an inner function access outer function variables?

Yes. An inner function can access variables from its own scope and its outer scopes.

### Q4. Can an outer function access variables from an inner function?

No. Variables declared inside an inner function are not directly accessible from the outer function.

### Q5. What is the scope chain?

The scope chain is the mechanism JavaScript uses to search for variables. It searches in the current scope and then in its outer scopes until it finds the variable or reaches the global scope.

### Q6. What is the relationship between lexical scope and closure?

Lexical scope defines where a function can access variables. Closures allow a function to retain access to variables from that lexical environment even after the outer function finishes executing.

---

## 9. Interview Answer

Lexical scope in JavaScript means the accessibility of variables is determined by where functions and blocks are defined in the source code, rather than where they are called.

An inner function can access variables from its own scope and the outer scopes. JavaScript searches for variables through the scope chain.

Lexical scope is also the foundation of closures in JavaScript.

---

## 10. Quick Revision

- Lexical scope is determined by where code is written.
- JavaScript uses lexical scope.
- Functions access variables based on their definition location.
- Inner functions can access outer function variables.
- Outer functions cannot directly access inner function variables.
- JavaScript searches for variables through the scope chain.
- Lexical scope is the foundation of closures.

### Remember This

**Where a function is written determines which variables it can access, not where the function is called.**



# JavaScript `this` Keyword

## 1. What is `this` in JavaScript?

The `this` keyword refers to the context in which a function is called.

In simple words, `this` helps a function identify who is calling it.

**For regular functions, the value of `this` depends on how the function is called, not where the function is written.**

---

## 2. `this` Inside an Object

```javascript
const person = {
  name: "Vipul",

  greet: function () {
    console.log(this.name);
  }
};

person.greet();
```

### Output

```text
Vipul
```

### Explanation

1. We created an object called `person`.
2. It contains a property called `name`.
3. We created a method called `greet()`.
4. Inside `greet()`, we used `this.name`.
5. We called the function using `person.greet()`.

Since `person` is calling the method, `this` refers to the `person` object.

Therefore:

```javascript
this.name
```

is equivalent to:

```javascript
person.name
```

---

## 3. `this` Inside a Regular Function

```javascript
function greet() {
  console.log(this);
}

greet();
```

The value of `this` depends on whether strict mode is enabled and on the execution environment.

### In Strict Mode

```javascript
"use strict";

function greet() {
  console.log(this);
}

greet();
```

### Output

```text
undefined
```

### Explanation

When a regular function is called without an object in strict mode, `this` is `undefined`.

In non-strict browser scripts, a standalone regular function generally has `this` referring to the global object.

---

## 4. `this` Inside a Nested Regular Function

```javascript
const person = {
  name: "Vipul",

  greet: function () {
    console.log(this.name);

    function inner() {
      console.log(this.name);
    }

    inner();
  }
};

person.greet();
```

### Output in a Non-Strict Browser Script

```text
Vipul
undefined
```

### Explanation

1. `person.greet()` is called.
2. `this` inside `greet()` refers to `person`.
3. The `inner()` function is called separately.
4. `inner()` is called as a standalone function.
5. Therefore, `this` inside `inner()` does not automatically refer to `person`.

In a strict-mode context, `this` inside `inner()` would be `undefined`.

**A nested regular function does not automatically inherit `this` from its parent function.**

---

## 5. `this` Inside an Arrow Function

Arrow functions do not have their own `this`.

They inherit `this` from their surrounding lexical scope.

### Example

```javascript
const person = {
  name: "Vipul",

  greet: function () {
    const inner = () => {
      console.log(this.name);
    };

    inner();
  }
};

person.greet();
```

### Output

```text
Vipul
```

### Explanation

1. `person.greet()` is called.
2. `this` inside `greet()` refers to `person`.
3. `inner` is an arrow function.
4. Arrow functions do not create their own `this`.
5. The arrow function inherits `this` from `greet()`.
6. Therefore, `this.name` prints `Vipul`.

---

## 6. Regular Function vs Arrow Function

| Regular Function | Arrow Function |
|---|---|
| Has its own `this` binding. | Does not have its own `this`. |
| `this` depends on how the function is called. | `this` comes from the surrounding lexical scope. |
| Can use `call()`, `apply()` and `bind()` to set its `this`. | Cannot replace its inherited `this` using `call()`, `apply()` or `bind()`. |
| Commonly used for object methods. | Useful for callbacks and nested functions. |

### Example

```javascript
const person = {
  name: "Vipul",

  regular: function () {
    console.log(this.name);
  },

  arrow: () => {
    console.log(this.name);
  }
};

person.regular();
person.arrow();
```

### Explanation

- `regular()` is called through `person`, so its `this` refers to `person`.
- `arrow()` does not have its own `this`.
- It uses the `this` from the surrounding lexical scope, not `person`.

**Avoid using arrow functions as object methods when you expect `this` to refer to the object itself.**

---

## 7. `this` With `call()`

The `call()` method allows us to specify what `this` should refer to when a function executes.

```javascript
function greet() {
  console.log("Hello " + this.name);
}

const person = {
  name: "Vipul"
};

greet.call(person);
```

### Output

```text
Hello Vipul
```

### Explanation

```javascript
greet.call(person);
```

Here, we explicitly tell JavaScript to execute `greet()` with `this` referring to `person`.

---

## 8. `this` With `apply()`

The `apply()` method works similarly to `call()`, but it accepts function arguments through an array-like argument list.

```javascript
function introduce(city, role) {
  console.log(this.name + " from " + city + " is a " + role);
}

const person = {
  name: "Vipul"
};

introduce.apply(person, ["Nagpur", "Developer"]);
```

### Output

```text
Vipul from Nagpur is a Developer
```

### Explanation

- The first argument specifies what `this` should refer to.
- The second argument is an array-like argument list containing the function arguments.

---

## 9. `this` With `bind()`

The `bind()` method creates a new function with a fixed `this` value.

```javascript
function greet() {
  console.log("Hello " + this.name);
}

const person = {
  name: "Vipul"
};

const newFunction = greet.bind(person);

newFunction();
```

### Output

```text
Hello Vipul
```

### Explanation

`bind()` does not immediately execute the function.

Instead, it returns a new function where `this` is bound to `person`.

---

## 10. Difference Between `call()`, `apply()` and `bind()`

| Method | Description |
|---|---|
| `call()` | Executes the function immediately with a specified `this` and individual arguments. |
| `apply()` | Executes the function immediately with a specified `this` and an array-like argument list. |
| `bind()` | Returns a new function with a specified `this` value. |

---

## 11. `this` Inside JavaScript Classes

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Hello " + this.name);
  }
}

const person = new Person("Vipul");

person.greet();
```

### Output

```text
Hello Vipul
```

### Explanation

1. We created a class called `Person`.
2. The constructor receives a `name`.
3. `this.name = name` stores the name on the new instance.
4. We created an object using `new Person("Vipul")`.
5. When `person.greet()` is called, `this` refers to the `person` instance.

---

## 12. How to Determine `this` in an Interview?

When an interviewer gives you a `this` question, follow these steps:

1. Is it a regular function or an arrow function?
2. If it is a regular function, how is it being called?
3. Is it called through an object, like `obj.method()`?
4. Is it called as a standalone function?
5. Is `call()`, `apply()` or `bind()` used?
6. Is the function being called using `new`?

### Quick Reference

| Situation | Value of `this` |
|---|---|
| `obj.method()` | `obj` |
| Standalone regular function in strict mode | `undefined` |
| Standalone regular function in a non-strict browser script | Global object |
| Arrow function | Inherited from surrounding lexical scope |
| Function called with `new` | Newly created instance |
| `call()` | Explicitly provided object |
| `apply()` | Explicitly provided object |
| `bind()` | Bound object |

---

## 13. Interview Questions

### Q1. What is `this` in JavaScript?

The `this` keyword refers to the context determined by how a function is invoked. For regular functions, its value is generally determined by the call site.

### Q2. What is the difference between `this` in a regular function and an arrow function?

A regular function has its own `this` binding, which depends on how it is called. An arrow function does not have its own `this`; it inherits `this` from its surrounding lexical scope.

### Q3. Can we change `this` in an arrow function using `bind()`?

No. Arrow functions inherit `this` from their surrounding scope. Their `this` cannot be replaced using `bind()`, `call()` or `apply()`.

### Q4. What is `bind()`?

`bind()` creates a new function with a fixed `this` value and can also preset some arguments.

### Q5. What is the difference between `call()`, `apply()` and `bind()`?

- `call()` executes a function immediately with a specified `this` and individual arguments.
- `apply()` executes a function immediately with a specified `this` and an array-like argument list.
- `bind()` returns a new function with a specified `this` value.

### Q6. What does `this` refer to inside a constructor?

When a constructor function is called using `new`, `this` refers to the newly created instance.

---

## 14. Quick Revision

- `this` depends on how a regular function is called.
- In `obj.method()`, `this` generally refers to `obj`.
- In a standalone regular function, `this` is `undefined` in strict mode.
- Arrow functions do not have their own `this`.
- Arrow functions inherit `this` from the surrounding lexical scope.
- `call()` executes a function with a specified `this`.
- `apply()` executes a function with a specified `this` and array-like arguments.
- `bind()` returns a function with a fixed `this`.
- In a constructor called with `new`, `this` refers to the new instance.

---

## 15. Remember This

**Regular Function:**

`this` depends on how the function is called.

**Arrow Function:**

`this` comes from its surrounding lexical scope.

**Object Method:**

When called as `object.method()`, `this` generally refers to the object.

**call, apply and bind:**

They help control `this` for regular functions.







