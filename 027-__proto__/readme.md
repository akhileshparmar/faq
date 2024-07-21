# `__proto__`

`__proto__` is a property available on all objects in JavaScript that points to the prototype of the object. It is part of the ECMAScript standard and provides a way to access or set the prototype (i.e., the `[[Prototype]]` internal slot) of an object.

### Usage of `__proto__`

1. **Accessing the Prototype of an Object**:

   ```javascript
   let obj = {};
   let prototype = obj.__proto__;
   console.log(prototype); // Object.prototype
   ```

2. **Setting the Prototype of an Object**:
   ```javascript
   let obj = {};
   let newProto = { someProperty: "value" };
   obj.__proto__ = newProto;
   console.log(obj.someProperty); // 'value'
   ```

### Key Points About `__proto__`

1. **Prototype Chain**:

   - `__proto__` is used to build and access the prototype chain. When a property is accessed on an object, JavaScript looks up the prototype chain using `__proto__` until it finds the property or reaches `null`.

2. **Legacy and Modern Alternatives**:

   - Although `__proto__` is widely supported and used, it is considered a legacy feature and not recommended for use in modern JavaScript code.
   - Instead, `Object.getPrototypeOf` and `Object.setPrototypeOf` are the preferred methods for getting and setting the prototype of an object.

     ```javascript
     let obj = {};
     let prototype = Object.getPrototypeOf(obj);
     console.log(prototype); // Object.prototype

     let newProto = { someProperty: "value" };
     Object.setPrototypeOf(obj, newProto);
     console.log(obj.someProperty); // 'value'
     ```

3. **ECMAScript Specification**:
   - The `__proto__` property is defined as an accessor property on `Object.prototype` with getter and setter functions. This allows all objects to inherit `__proto__` and use it to access their prototype.
   - Using `__proto__`, you can dynamically change the prototype of an existing object, but this is generally discouraged due to potential performance issues and the complexity it can introduce into the code.

### Example

```javascript
let animal = {
  eats: true,
};

let rabbit = {
  jumps: true,
};

rabbit.__proto__ = animal;

console.log(rabbit.eats); // true
console.log(rabbit.jumps); // true
```

In this example, the `rabbit` object has `animal` as its prototype, so it can access properties defined on `animal`.

### Summary

- `__proto__` is a property that points to the prototype of an object.
- It is used to access and set the prototype, playing a crucial role in the prototype chain.
- `__proto__` is considered a legacy feature; `Object.getPrototypeOf` and `Object.setPrototypeOf` are recommended for modern code.
- Modifying prototypes dynamically using `__proto__` can lead to performance issues and complex code, so it should be used with caution.
