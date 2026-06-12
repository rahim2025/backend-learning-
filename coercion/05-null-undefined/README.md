# null and undefined Traps

Loose equality has a special rule:

```js
null == undefined; // true
null === undefined; // false
null == 0; // false
null == false; // false
undefined == false; // false
```

Do not say `==` always converts everything to numbers. In loose equality, `null` is only loosely equal to `undefined`.

Arithmetic context is different:

```js
null + 1; // 1
undefined + 1; // NaN
Number(null); // 0
Number(undefined); // NaN
```

