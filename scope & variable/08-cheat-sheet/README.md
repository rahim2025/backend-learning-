# Scope and Variables Cheat Sheet

## Scope

- Scope means where a variable is accessible.
- Inner scope can access outer scope.
- Outer scope cannot access inner scope.

## `var`, `let`, and `const`

| Keyword | Scope | Reassign? |
| --- | --- | --- |
| `var` | Function/global | Yes |
| `let` | Block | Yes |
| `const` | Block | No |

## Hoisting

| Declaration | Before declaration line |
| --- | --- |
| `var` | `undefined` |
| `let` | ReferenceError because of TDZ |
| `const` | ReferenceError because of TDZ |
| Function declaration | Fully available |
| Function expression | Function value not available yet |

## TDZ

TDZ means the variable exists but cannot be accessed before the declaration line.

```js
{
  console.log(age); // ReferenceError
  let age = 20;
}
```

## `const`

```js
const user = { name: "Rahim" };

user.name = "Karim"; // allowed
user = {}; // TypeError
```

`const` prevents reassignment of the binding, not mutation of the object.

## Lexical Scoping

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

A function uses the scope where it was written, not where it was called.

