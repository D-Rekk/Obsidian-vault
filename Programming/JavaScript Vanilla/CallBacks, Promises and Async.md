# JavaScript 06. Async

Created: July 29, 2022 6:11 PM
Status: Open
URL: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing
Updated: November 29, 2022 6:36 PM

[Asynchronous Programming](Asynchronous%20Programming.md)

## CallBacks

What is a callaback? A `callback` is a **function** referenced as *parameter* inside another function and invoked inside this last one. The latter function is known as higherOrderFunction.

```jsx
function add (x,y) {return x+y}
function addFive(a,addReference)
	{return add(a,5)}
addFive(10,add) //15
```

```jsx
//Syntactically would be:
function hiOrderFunction(a,callback)
	{return callback(a,5)}
addFive(10,add) //15
```

## Promises

`Promises` is one among the firsts implementation of callbacks. They exist making the complexity of asynchronous requests more managable.

> *They are objects returned by an asynchronous function which represents the current state of the operation.*
> 

Asynchronous request with promises has three status:

1. pending. Is the default, initial state. When you call a function, it’s in this state.
2. fullfilled. Is the expected result of the async request being successful
3. rejected. Is the state that calls an error when something goes wrong.

### How to implement promises in JS

To create a promise you simple call the constructor `Promise`.
It accepts a single callback function. This latter accepts two parameters, a `resolve` and a `reject` callbacks functions. 

```jsx
let myPromise = new Promise (); //becomes...
let myPromise = new Promise ((resolve, reject) => {
})
```

`resolve` changes the status of the async request to fullfilled, while when `reject` is invoked the status of the promise becomes rejected.

### How to listen when promise status changes?

When the promise status changes to fullfilled (which it will when we call the resolve argument), the function that you pass in `.then()` is going to be invoked.

Instead when the status change to rejected (which it will when if we call reject), the function that you pass in `.catch()` is going to be invoked.

```jsx
function onResolve ()
	{console.log('Resolved!')}
function onReject ()
	{console.log('RIP, Rejected')}
//                         fullfilled, rejected
const promise = new Promise ((resolve, reject) => {
	setTimeout (() => {
		{...}       //some code
		resolve(); //Promise becomes fulfilled
	},2000);
}) 
```

```jsx
promise.then(onResolve); //returns onResolve when fulfilled
promise.catch(onReject); //returns onReject when rejected 
```

---

Another feature of promises that will make our code a little bit better is **chaining promises**. Everytime you call `.then` method *you create a new Promise*.

```jsx
const url = "jsonplaceholder.typicode.com/todos/1";
fetch(url)
	.then((res) => {
		return res.json();
	})
	.then((data) => {
		console.log(data);
	})
	.catch((err) => {
	 console.error(err);
	}
```

# Async/Await

The above code doesn’t allow you to access the previous arguments once they’re returned. **Async** is a new build-in method in ECMAScript6 that *permits you to manage asynchronous calls as if they were synchronous*.

```jsx
const LoadData = async () => {
	
	try{
 //saving return promise in a variable
		const url = "jsonplaceholder.typicode.com/todos/1";
		const res = await fetch(url); 
		const data = await res.json();
		return data; //this returns a promise (bc it's asynchronous)
	}catch(eventualErr){
		console.error(eventualErr) //return when value not fulfilled
	}
}
```

```jsx
let data = LoadData(); //empty bc memorized while pending
console.log(data);  // {}
//since it's async, we should access through .then
let data = LoadData().then( data => console.log(data)); 
```

We declare a function with `async` keywork, then store our arrow function in a variable. Instead of using `.then` method, we’ll use `await` keywork to access the return result (previously stored in a varialbe).

This makes the code much mode cleaner to debug. Yet there’s no method implemented to store an eventual error (`.catch` is not being replaced). What we can do is wrap our code in a `try/catch` function.

---

### Top-Level Async/Await with IIFE

**IIFE** (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it’s defined. 

```jsx
( async () => {
	const data = await LoadData ();
	console.log(data);
}) (); // () calls the function itself
```

---

```jsx
*/code here/*
```

---

<aside>
💡

</aside>

 Something

---