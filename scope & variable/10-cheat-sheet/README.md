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

## Closures

```txt
Closure = function + remembered outer variables
```

Closures come from lexical scoping.

Closures can:

- Preserve state.
- Create private variables.
- Let callbacks remember outer variables.
- Create a new remembered environment for each function call.

```js
function createCounter() {
  let count = 0;

  return function increment() {
    count++;
    return count;
  };
}

const counter = createCounter();

counter(); // 1
counter(); // 2
```

## Async Loop Trap

`var` shares one variable:

```js
for (var i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}

// 4
// 4
// 4
```

`let` creates a new variable per iteration:

```js
for (let i = 1; i <= 3; i++) {
  setTimeout(function () {
    console.log(i);
  }, 1000);
}

// 1
// 2
// 3
```

## `this`

`this` is usually decided by how a function is called.

```txt
this is decided by the call site
```

## Global `this`

Global `this` depends on the environment.

```js
console.log(this); // browser script: window
console.log(this); // Node CommonJS file: {}
```

## `this` Inside Object Method

```js
const user = {
  name: "Rahim",
  greet() {
    return this.name;
  }
};

user.greet(); // "Rahim"
```

In `user.greet()`, `this` is `user`.

## Losing `this`

```js
const greet = user.greet;

greet(); // loses this
```

Fix:

```js
const boundGreet = user.greet.bind(user);

boundGreet(); // "Rahim"
```

## Arrow Functions and `this`

Arrow functions do not have their own `this`.

They capture `this` from the surrounding scope.

```js
const user = {
  name: "Rahim",
  greet: () => this.name
};

user.greet(); // usually undefined
```

Do not use arrow functions as object methods when you need `this` to be the object.

## `this` Inside Nested Functions

Regular nested functions have their own `this`.

```js
const user = {
  name: "Rahim",
  outer() {
    function inner() {
      return this.name;
    }

    return inner();
  }
};

user.outer(); // TypeError in strict mode, or undefined
```

Use an arrow function to keep the outer `this`:

```js
const user = {
  name: "Rahim",
  outer() {
    const inner = () => this.name;

    return inner();
  }
};

user.outer(); // "Rahim"
```
