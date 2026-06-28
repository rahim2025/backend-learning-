# Object-Oriented Programming in JavaScript

This chapter contains notes about object-oriented programming (OOP), factory functions, constructor functions, and prototypes in JavaScript.

JavaScript is a prototype-based language. It can still use familiar OOP ideas such as objects, encapsulation, inheritance, and polymorphism, but it implements inheritance through prototypes.

## Topics

1. [What Is OOP?](01-what-is-oop/README.md)
2. [Factory Functions](02-factory-functions/README.md)
3. [Constructor Functions](03-constructor-functions/README.md)
4. [Prototypes](04-prototypes/README.md)

## The Main Idea

Suppose an application needs many user objects. Creating each object manually repeats code:

```js
const user1 = {
  name: "Rahim",
  login() {
    console.log(`${this.name} logged in`);
  },
};

const user2 = {
  name: "Karim",
  login() {
    console.log(`${this.name} logged in`);
  },
};
```

Object-creation patterns solve this repetition:

- A **factory function** creates and returns an object.
- A **constructor function** works with `new` to create an object.
- A **prototype** lets objects share properties and methods.

## Quick Comparison

| Feature | Factory function | Constructor function |
| --- | --- | --- |
| Called with `new` | No | Yes |
| Returns object explicitly | Usually yes | Usually no |
| Naming convention | camelCase | PascalCase |
| Uses `this` | Optional | Usually yes |
| Shared methods | Can use a shared object | Usually placed on `.prototype` |

## Interview Summary

OOP organizes programs around objects that contain data and behavior. In JavaScript, factory functions and constructor functions are two ways to create multiple similar objects. Factory functions return objects directly, while constructor functions are called with `new`. JavaScript uses prototypes so objects can share methods instead of storing a separate method copy on every object.
