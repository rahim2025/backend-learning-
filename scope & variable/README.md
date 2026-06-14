# JavaScript Scope and Variables

This folder contains backend interview notes about JavaScript scope, variable declarations, hoisting, TDZ, `const`, and lexical scoping.

Scope and variables are important for backend development because they affect how data is shared, hidden, updated, and captured inside functions, route handlers, callbacks, and modules.

## Topics

1. [Scope](01-scope/README.md)
2. [`var`, `let`, and `const`](02-var-let-const/README.md)
3. [Hoisting](03-hoisting/README.md)
4. [Temporal Dead Zone](04-tdz/README.md)
5. [`const` Does Not Mean Immutable](05-const-mutability/README.md)
6. [Lexical Scoping](06-lexical-scoping/README.md)
7. [Interview Questions](07-interview-questions/interview-questions.md)
8. [Cheat Sheet](08-cheat-sheet/README.md)

## 1. Scope

Scope means where a variable is accessible.

```js
const globalName = "Rahim";

function greet() {
  const message = "Hello";
  console.log(globalName); // allowed
  console.log(message); // allowed
}

greet();
console.log(message); // ReferenceError
```

Inner scope can access outer scope.

Outer scope cannot access inner scope.

| Rule | Example |
| --- | --- |
| Inner can access outer | A function can read a global variable |
| Outer cannot access inner | Global code cannot read a variable declared inside a function |

## 2. `var`, `let`, and `const`

| Keyword | Scope | Reassign? | Redeclare in same scope? |
| --- | --- | --- | --- |
| `var` | Function/global scoped | Yes | Yes |
| `let` | Block scoped | Yes | No |
| `const` | Block scoped | No | No |

`var` ignores block scope:

```js
if (true) {
  var x = 1;
}

console.log(x); // 1
```

`let` and `const` stay inside blocks:

```js
if (true) {
  let y = 2;
}

console.log(y); // ReferenceError
```

This is the key distinction:

- `var` is function/global scoped.
- `let` and `const` are block scoped.

Backend preference:

- Use `const` by default.
- Use `let` when reassignment is needed.
- Avoid `var` in modern backend JavaScript.

## 3. Hoisting

Hoisting means JavaScript processes declarations before code execution.

| Declaration | Hoisted? | Initialized before declaration line? |
| --- | --- | --- |
| `var` | Yes | Yes, as `undefined` |
| `let` | Yes | No, TDZ |
| `const` | Yes | No, TDZ |
| Function declaration | Yes | Yes, full function is available |
| Function expression | Variable is hoisted | Function value is not hoisted |

`var` example:

```js
console.log(a); // undefined
var a = 10;
```

This behaves like:

```js
var a;
console.log(a); // undefined
a = 10;
```

`let` example:

```js
console.log(b); // ReferenceError
let b = 10;
```

Function declaration:

```js
sayHello(); // "Hello"

function sayHello() {
  return "Hello";
}
```

Function expression:

```js
sayHi(); // TypeError or ReferenceError depending on declaration style

var sayHi = function () {
  return "Hi";
};
```

With `var`, the variable exists as `undefined`, but the function value is assigned later.

## 4. TDZ

TDZ means Temporal Dead Zone.

The variable exists, but you cannot access it before the declaration line.

```js
{
  console.log(age); // ReferenceError
  let age = 20;
}
```

The TDZ starts at the beginning of the block and ends at the declaration line.

```js
{
  // TDZ starts here
  // age exists, but cannot be used

  let age = 20; // TDZ ends here
  console.log(age); // 20
}
```

`let` and `const` have TDZ. `var` does not behave the same way because it is initialized as `undefined`.

## 5. `const` Does Not Mean Immutable

`const` prevents reassignment of the variable binding.

It does not freeze the value.

```js
const user = { name: "Rahim" };

user.name = "Karim"; // allowed

user = {}; // TypeError
```

Why?

- `user` still points to the same object.
- Mutating `user.name` changes the object.
- Assigning `user = {}` tries to point the binding to a new object, which is not allowed.

**Interview sentence:**

> `const` prevents reassignment of the binding, not mutation of the object.

To make an object harder to mutate, use tools like `Object.freeze()`:

```js
const user = Object.freeze({ name: "Rahim" });

user.name = "Karim"; // ignored in non-strict mode, TypeError in strict mode
```

## 6. Lexical Scoping

Lexical scoping means a function uses the scope where it was written, not where it was called.

```js
let value = "global";

function getValue() {
  return value;
}

function run() {
  let value = "local";
  return getValue();
}

run(); // "global"
```

Why?

`getValue()` was written in the global scope, so it remembers the global `value`.

It does not use the `value` inside `run()` just because `run()` called it.

This matters in backend JavaScript when callbacks and helper functions read variables from outer scopes.

## Interview Summary

If an interviewer asks about scope and variables, a strong answer should mention:

- Scope controls where variables can be accessed.
- Inner scopes can access outer scopes, but outer scopes cannot access inner scopes.
- `var` is function/global scoped.
- `let` and `const` are block scoped.
- `var` is hoisted and initialized as `undefined`.
- `let` and `const` are hoisted but inaccessible during the TDZ.
- Function declarations are fully hoisted.
- Function expressions are not fully available until assignment.
- `const` prevents reassignment, not object mutation.
- Lexical scoping is based on where a function is written.

