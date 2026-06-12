# Floating Point Precision

```js
0.1 + 0.2 === 0.3; // false
```

This is not a coercion issue. It is a floating-point precision issue caused by binary representation of decimal fractions.

Safe comparison:

```js
Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON;
```

For backend money calculations, use integer cents, a decimal library, or database decimal types.

