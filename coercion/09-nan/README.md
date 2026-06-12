# NaN Traps

`NaN` means "Not a Number", but its type is number.

```js
typeof NaN; // "number"
NaN == NaN; // false
NaN === NaN; // false
NaN !== NaN; // true
Number.isNaN(NaN); // true
```

`NaN` is never equal to itself.

| Expression | Result |
| --- | --- |
| `isNaN("hello")` | `true` |
| `Number.isNaN("hello")` | `false` |
| `isNaN(undefined)` | `true` |
| `Number.isNaN(undefined)` | `false` |

`isNaN()` coerces first. `Number.isNaN()` does not coerce and is safer after explicit conversion.

