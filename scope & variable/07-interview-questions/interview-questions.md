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

