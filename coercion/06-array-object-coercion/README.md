# Array and Object Coercion

Objects and arrays use `ToPrimitive` when JavaScript needs a primitive value.

```js
[].toString(); // ""
[1, 2].toString(); // "1,2"
({}).toString(); // "[object Object]"
```

Examples:

```js
[] + []; // ""
[] + {}; // "[object Object]"
[1] + [2]; // "12"
[1, 2] + [3, 4]; // "1,23,4"
[1, 2] == "1,2"; // true
[0] == false; // true
```

`ToPrimitive` checks `Symbol.toPrimitive`, then conversion methods such as `valueOf()` and `toString()` depending on the hint.

