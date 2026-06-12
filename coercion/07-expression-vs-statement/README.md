# Expression Context vs Statement Context

This is a parsing trap:

```js
[] + {}; // "[object Object]"
{} + []; // 0 at statement level
({} + []); // "[object Object]"
```

At the beginning of a statement, `{}` can be parsed as an empty block, not an object expression.

```js
{} + []
```

can be parsed like:

```js
{}; +[]
```

Then `+[]` becomes `0`.

Inside parentheses, `{}` must be an object expression:

```js
({} + []); // "[object Object]"
```

