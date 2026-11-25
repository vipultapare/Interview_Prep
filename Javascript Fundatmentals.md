
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

