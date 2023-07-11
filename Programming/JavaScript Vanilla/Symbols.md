# Javascript 08. Symbols

Created: November 24, 2022 7:47 PM
Status: Open
URL: https://dev.to/lioness100/javascript-symbols-classes-2b08
Updated: January 10, 2023 1:38 PM

## Immutability

There are essentially **two** types of values in JavaScript. 
First type is **primitives**, second type is **objects** (including functions).

Primitive values include simple values types, such as *numbers* (ranging from floats to NaN), *booleans*, *strings*, *undefined* and *null*.

Primitive have this properties called **immutability**. They can’t be changed. Of course, a variable *can* be reassigned, but variables hold **reference** to the primitive value, and this last one *cannot* be changed.

```jsx
let name = 'Snderson' // small typo
name[0] = 'A' // Accessing string at [0] to change value
console.log(name) // output: 'Snderson'
```

A string in `name[0]`,  *pointing* to the first value of the string, is not mutable. Even though we redeclare a new value for it, the original string has **remained the same**.

## Memory Management

**JavaScript engine have two places to store data:**

- **Stack**: It is a data structure used to store static data. Static data refers to data whose size is known by the engine during compile time. Static data include primitives and *references* to objects and functions. A fixed amount, known as **static memory allocation**, is used for static data.
- **Heap**: It is used to store objects and functions in JavaScript. The engine doesn’t allocate a fixed memory since size is known at run time, also know as **dynamic memory allocation**.

All variable are stored in stack. If the value is an object, the **Stack** **reference** is pointing the **Heap data**.

[https://www.figma.com/file/qm8ezKEmRUYmAY4xC4lTu3/Stack%2FHeap?node-id=0%3A1&t=3vPSsZNsmrpkMVeB-1](https://www.figma.com/file/qm8ezKEmRUYmAY4xC4lTu3/Stack%2FHeap?node-id=0%3A1&t=3vPSsZNsmrpkMVeB-1)

```jsx
const User = {
	name: 'Anderson',
	age: 21
};  
const name = 'Andy';

function getName(name){
	return name;
}

const newUser = User;
```

Unlike low-level languages like **C**, JavaScript automatically allocates memory when objectes are created and frees it when not in use anymore. This is called **garbage collection**.

---

### Passing a variable:
Pass-by-value & Pass-by-reference

Some languages, such as C, have the concept of **pass-by-value** and **pass-by-reference**. These terms are used to describe how variables are passed on a function.

**Passing by value** means that the value of the function parameter is copied into another location of your memory. When accessing or modifying the variable within your function, only the copy is modified, the original value is left untouched.

**Passing by reference** means that the memory address of the variable (a pointer) is passed to the function.  This means that it’s possible to change one or more variables within the function.

> In **JavaScript**, pass-by-value occurs with primitive value, while pass-by-reference happens when passing objects.
> 

```jsx
function primitiveMutator(val) {
  val = val + 1;
}
function objectMutator(val) {
  val.prop = val.prop + 1;
}
let x = 1;
let obj = { prop: 1 };
primitiveMutator(x); // x = 1
objectMutator(obj); // obj.prop = 2
```

Constructing equivalent non-primitive (object) values *will not* result in values which are exactly equal, because they’re *pointing* to different **Heap data**. 

```jsx
const obj1 = { name: "Intrinsic" };
const obj2 = { name: "Intrinsic" };
console.log(obj1 === obj2); // false
```

---

## Symbols

The original motivation for introducing symbols to JavaScript was to enable *private* properties.

Objects play an elemental role in the JavaScript language. They’re used *everywhere* as collection of key/value pairs. However, there’s a big limitation of using them in this manner, Until symbols existed, **objects key could only be strings**. If we ever attempt to use a non-string value as key for an object, the value will be coerced to a string. 

```jsx
const obj = {}
obj['bar'] = 'bar';
obj[2] = 2;
obj[{}] = 'someobj';
console.log(obj);
/* output _>
{ bar: 'bar',
	'2': 2,
	'[object Object]' : 'someobj'
} */
```

### What is a Symbol

**A symbol is a primitive which cannot be recreated**. 

A symbol is similar to an object as creating multiple instances will result in values which are not exactly equal. But a symbol is also a primitive that **cannot be mutated**.

```jsx
const s1 = Symbol();
const s2 = Symbol();
s1 === s2 // false
```

When initializing a symbol, there’s an optional first argument where you can choose to provide a string. This value is intended to be descriptive, used for *debugging purpose.* It doesn’t really affect the symbol itself.

Symbols have an important use. They can be used as **unique keys** in objects.

```jsx
const obj = {};
const sym = Symbol();
obj[sym] = 'foo';
obj.bar = 'bar';
console.log(obj, // {bar : 'bar'}
						sym in obj, //true
						obj[sym], //foo
						Object.keys(obj), //['bar']
						Object.getOwnPropertySymbols(obj), // Symbol()
						Reflect.ownKeys(obj), //['bar', Symbol()] 
						obj[Reflect.ownKeys(obj)[1]) //'foo'
```

At first glance, one of the reasons of adding a new data type was to enable **private properties** in JavaScript. Unofortunately, it is still possible for code which interacts with this object to access properties-symbols.

Since every symbol is unique, and in no way can two symbols be equal to each other, **libraries** can add properties to objects without the risk of having name collisions

```jsx
function lib1tag(obj) {
  obj.id = 42;
}
function lib2tag(obj) {
  obj.id = 369;
} //collision of metadata
```

By making use of symbols, each library can generate their required symbols upon instantiation.

```jsx
const library1property = Symbol('lib1');
function lib1tag(obj) {
  obj[library1property] = 42;
}
const library2property = Symbol('lib2');
function lib2tag(obj) {
  obj[library2property] = 369;
}
```

---

Another of the main advantages of using Symbols in JavaScript is the **performance advantages** over strings. Every time you use the string notation, a new object gets created in the memory heap while symbols remain always the same during the execution of the program. In JavaScript we can replicate this behaviour by creating a symbol in the global registry.

---

<aside>
💡

</aside>

 Something

---