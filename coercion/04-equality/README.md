# `==` vs `===`

`===` compares without coercion. `==` follows the Abstract Equality Comparison rules and may coerce.

| Expression | Result |
| --- | --- |
| `0 == false` | `true` |
| `0 === false` | `false` |
| `"0" == false` | `true` |
| `Boolean("0")` | `true` |
| `[] == false` | `true` |
| `Boolean([])` | `true` |
| `{} == false` | `false` |
| `Boolean({})` | `true` |

Boolean context and loose equality context are different.

```js
Boolean([]); // true
[] == false; // true
```

`Boolean([])` uses `ToBoolean`, where all objects are truthy. `[] == false` uses loose equality, where `[]` becomes `""`, then `0`, and `false` becomes `0`.

