# Abstract Operations

JavaScript uses internal conversion operations behind the scenes.

| Operation | Purpose |
| --- | --- |
| `ToPrimitive` | Converts objects to primitives |
| `ToNumber` | Converts values to numbers |
| `ToString` | Converts values to strings |
| `ToBoolean` | Converts values to booleans |

## ToNumber

| Expression | Result |
| --- | --- |
| `Number("")` | `0` |
| `Number(" ")` | `0` |
| `Number("42")` | `42` |
| `Number("abc")` | `NaN` |
| `Number(null)` | `0` |
| `Number(undefined)` | `NaN` |
| `Number([])` | `0` |
| `Number({})` | `NaN` |

## ToBoolean

Only these values are falsy:

```js
false
0
""
null
undefined
NaN
```

Everything else is truthy, including `"0"`, `"false"`, `[]`, `{}`, and `" "`.

