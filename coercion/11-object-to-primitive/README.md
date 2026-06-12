# Object to Primitive Conversion

`Symbol.toPrimitive` has highest priority.

| Hint | Order |
| --- | --- |
| `number` | `valueOf()` first, then `toString()` |
| `string` | `toString()` first, then `valueOf()` |
| `default` | Usually behaves like number for normal objects |

```js
const obj = {
  valueOf() {
    return 10;
  },
  toString() {
    return "20";
  }
};

+obj; // 10
String(obj); // "20"
```

Fallback example:

```js
const obj = {
  valueOf() {
    return {};
  },
  toString() {
    return "7";
  }
};

+obj; // 7
```

Failure example:

```js
const obj = {
  valueOf() {
    return {};
  },
  toString() {
    return {};
  }
};

+obj; // TypeError: Cannot convert object to primitive value
```

