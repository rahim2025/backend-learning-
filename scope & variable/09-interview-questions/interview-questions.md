# JavaScript Scope and Variables Interview Questions

## Q: What is scope in JavaScript?

Scope means where a variable is accessible. Inner scopes can access variables from outer scopes, but outer scopes cannot access variables declared inside inner scopes.

## Q: What is the difference between `var`, `let`, and `const`?

`var` is function or global scoped. `let` and `const` are block scoped. `let` allows reassignment, while `const` does not allow reassignment of the binding.

## Q: Why does `var` work outside an `if` block?

Because `var` is not block scoped. It belongs to the nearest function scope or global scope.

```js
if (true) {
  var x = 1;
}

console.log(x); // 1
```

## Q: Why does `let` throw a `ReferenceError` outside an `if` block?

Because `let` is block scoped. It only exists inside the block where it is declared.

```js
if (true) {
  let y = 2;
}

console.log(y); // ReferenceError
```

## Q: What is hoisting?

Hoisting means JavaScript processes declarations before code execution. `var` is hoisted and initialized as `undefined`; `let` and `const` are hoisted but unavailable during the TDZ; function declarations are fully hoisted.

## Q: Why does `console.log(a)` print `undefined` before `var a = 10`?

Because `var a` is hoisted and initialized as `undefined`. The assignment `a = 10` happens later during execution.

```js
console.log(a); // undefined
var a = 10;
```

## Q: Why does `console.log(b)` throw before `let b = 10`?

Because `let` is hoisted but stays in the Temporal Dead Zone until the declaration line is executed.

```js
console.log(b); // ReferenceError
let b = 10;
```

## Q: What is TDZ?

TDZ means Temporal Dead Zone. It is the period from the start of a block until a `let` or `const` declaration is reached. During TDZ, the variable exists but cannot be accessed.

## Q: Does `const` make an object immutable?

No. `const` prevents reassignment of the binding, not mutation of the object.

```js
const user = { name: "Rahim" };
user.name = "Karim"; // allowed
user = {}; // TypeError
```

## Q: What is lexical scoping?

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

## Q: What is a closure?

A closure is a function that remembers variables from its outer lexical scope even after the outer function has finished executing.

```js
function outer() {
  const message = "Hello";

  return function inner() {
    return message;
  };
}

const fn = outer();

fn(); // "Hello"
```

`inner()` still remembers `message`, so `inner()` has a closure.

## Q: How do closures preserve state?

Closures preserve state because the inner function keeps access to variables from the outer function.

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

`count` stays alive between calls.

## Q: How can closures create private variables?

Closures can keep variables inside a function and expose only selected methods.

```js
function createSession() {
  let token = "abc123";

  return {
    getToken() {
      return token;
    }
  };
}

const session = createSession();

session.getToken(); // "abc123"
session.token; // undefined
```

`token` is private because outside code cannot access it directly.

## Q: Why do closures come from lexical scoping?

Because JavaScript functions use the scope where they are written. If an inner function is written inside an outer function, it can remember that outer function's variables.

## Q: Does each function call create a new closure?

Each function call can create a new closure if it returns or passes a function that remembers local variables from that call.

```js
const counterA = createCounter();
const counterB = createCounter();

counterA(); // 1
counterB(); // 1
```

`counterA` and `counterB` have separate remembered `count` variables.

## Q: Why does `var` in async loops often print the same value?

Because `var` is function scoped, all callbacks close over the same loop variable.

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

By the time the callbacks run, the loop has finished and `i` is `4`.

## Q: Why does `let` fix async loop closures?

Because `let` creates a new binding for each loop iteration.

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

Each callback remembers a different `i`.

## Q: What is `this` in JavaScript?

`this` is a special keyword whose value usually depends on how a function is called. It is decided by the call site.

## Q: What is global `this`?

Global `this` depends on the JavaScript environment. In a browser script, global `this` is usually `window`. In Node.js CommonJS files, top-level `this` is usually `{}`. In backend code, it is better to avoid depending on global `this`.

## Q: What is `this` inside an object method?

When a function is called as an object method, `this` points to the object before the dot.

```js
const user = {
  name: "Rahim",
  greet() {
    return this.name;
  }
};

user.greet(); // "Rahim"
```

Here, `this` is `user`.

## Q: How do we lose `this`?

We lose `this` when a method is separated from its object or passed as a callback.

```js
const greet = user.greet;

greet(); // loses this
```

The call no longer has `user` before the dot, so `this` is not `user`.

## Q: How can we fix lost `this`?

Use `bind`, an arrow wrapper, or call the method directly from the object.

```js
const boundGreet = user.greet.bind(user);

boundGreet(); // "Rahim"
```

```js
app.get("/users", (req, res) => controller.getUsers(req, res));
```

## Q: How do arrow functions handle `this`?

Arrow functions do not have their own `this`. They capture `this` from the surrounding scope.

This means arrow functions are usually not good object methods:

```js
const user = {
  name: "Rahim",
  greet: () => this.name
};

user.greet(); // usually undefined
```

But arrows are useful inside methods:

```js
const user = {
  name: "Rahim",
  hobbies: ["coding"],
  printHobbies() {
    this.hobbies.forEach((hobby) => {
      console.log(`${this.name} likes ${hobby}`);
    });
  }
};
```

The arrow callback keeps the method's `this`.

## Q: What happens to `this` inside nested regular functions?

Regular nested functions have their own `this`. They do not automatically inherit `this` from the outer method.

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

Use an arrow function when the nested function should keep the outer method's `this`.
