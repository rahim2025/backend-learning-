# What is Type Coercion?

Type coercion means JavaScript converts a value from one type to another.

| Kind | Meaning | Example |
| --- | --- | --- |
| Implicit coercion | JavaScript converts automatically. | `"5" - 2 // 3` |
| Explicit coercion | The developer converts intentionally. | `Number("5") // 5` |

```js
"5" - 2; // 3
"5" + 2; // "52"
Number("5"); // 5
```

Production backend code should prefer explicit coercion because request input is often string-based and hidden conversions can accept or reject the wrong values.

**Interview answer:** Type coercion is JavaScript converting values between types. Implicit coercion happens automatically through operators and contexts. Explicit coercion uses tools like `Number()`, `String()`, and `Boolean()`, and is preferred in validation because it makes edge cases visible.

