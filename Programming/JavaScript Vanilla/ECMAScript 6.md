# JavaScript 04: ECMAScript 6

Created: July 12, 2022 7:34 PM
Status: Open
Updated: February 8, 2023 7:06 PM

# ECMAScript 6

ECMAScript 6 refers to the standard. introduces in 2015 for JavaScript. It brought some major changes, from scoping to OOP methods.

---

### Variables

They follow the “modern” block-scoped rules. You can declare/initialize variables in two ways:

```jsx
const MAX = 100;
let value = 5;
```

The main difference is the possibility of re-definition. Once initialized, a **const** variable can’t change within the same scope. The variables declared with let can be changed at will.

### Arrow Function

Arrow function are a syntactically easier and shorter way to write a function.

```jsx
let group = {
  title: "Our Group",
  students: ["John", "Pete", "Alice"],

  const showList = () => {
    this.students.forEach(student =>
			alert(this.title + ': ' + student)
    );
  }
};
group.showList();
```

Arrow function **do not** have *“this”*. They actually refer to the outer instance. This means also that they can’t be called *new* in class constructor.

### Spread Operator

> [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) allows an iterable (i.e. an array) to be **expanded** in places where 0+ arguments (for function calls) or elements (for array literals) are expected. It also allows object expression to be expanded in places where 0+ key-value pairs are expected.
> 

**Spread** operator *opens* an array or an object, and *spreads* the content of it in the function or an object. It can be used when all elements from an object or array need to be included in a new array or object, or should be applied one-by-one in a function call's arguments list

```jsx
const nums = [9,3,2,8]
Math.max(nums); //NaN since it can't accept an array as argument
Math.max(...nums); //67 since argument is (9,3,2,8)

numsCopy = [1,5,...nums] //it can copy an concatenate arrays

```

---
## Props Destructuring

^476a5a

> **Destructuring** is an ES6 feature that allows us to extract multiple pieces of data from an array or object and assign them to their own variable. This is a huge upside in React when you’re passing down props. You can get rid of `props / this.props` in front of each prop.
> 

```jsx
let object = {
	one: 1,
	two: 2,
	three: 3 }

let one = object.one;
let two = object.two;
let three = object.three;
//Destructing would make it:
let {one,two,three} = object;
```
