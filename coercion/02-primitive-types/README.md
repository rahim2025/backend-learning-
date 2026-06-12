# JavaScript Primitive Types

JavaScript has 7 primitive types.

| Primitive | Example | Notes |
| --- | --- | --- |
| `string` | `"hello"` | Text |
| `number` | `42`, `NaN` | `NaN` is type number |
| `bigint` | `123n` | Large integers |
| `boolean` | `true` | Logical values |
| `undefined` | `undefined` | Declared but not assigned or missing |
| `null` | `null` | Intentional absence of value |
| `symbol` | `Symbol("id")` | Unique primitive |

```js
typeof NaN; // "number"
typeof null; // "object"
```

`null` means intentional absence. `undefined` usually means missing or not assigned.

