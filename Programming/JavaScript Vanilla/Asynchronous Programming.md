[Asynchronous programming](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing) is a technique that enables your program to start a potentially long-running task and still be able to be *responsive* to other events while that task runs, rather than having to wait until that task has finished.

---

### Synchronous programming

Consider the following code:


```jsx
const name = 'Miriam';
const greeting = `Hello, my name is ${name}!`;
console.log(greeting);
// "Hello, my name is Miriam!"
```

This code:

1. Declares a string called `name`
2. Declares another string called `greeting`, which uses `name`
3. Outputs the greeting to the console

> The browser effectively steps through the program one line at a time, in the order we wrote it. At each point, the browser waits for the current line to execute its work before going on the next line. That makes this a **synchronous program**.
> 

It would still be synchronous even if we called a separate function.

What if the function takes a long time? While executing a long-running function, our program is completely unresponsive: you can’t type, click, or do anything else.

This is the basic program with long-running synchronous functions. What we need is a way for our program to:

1. Start a long-running operation by calling a function.
2. **Have that function start the operation and return immediately**, so that our program can still be rensponsive to other events.
3. Notify us with the result of the operation when it eventually completes.

Modern asynchronous APIs don’t use callbacks, which are hard to read and debug once deeply nested (callback hell). Instead, the foundation of asynchronous progarmming in JavaScript is the `Promise` .

---

## Promises

A promise is an **object returned by an asynchronous function**, which represents the current state of the operation. At the time the promise is return to the caller, the operation often isn’t finished, but the promise object provides methods to handle the eventual success or failure of operation.

---

We’ll send a request to get a JSON file from the server using `fetch()` API, which is a modern promise-based method:

```jsx
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

console.log(fetchPromise);
//This happens only when state: ok (Asynchronously)
fetchPromise.then((response) => { //handler function (arrow fun)
  console.log(`Received response: ${response.status}`)
});

console.log("Started request…");
```

```jsx
Promise { <state>: "pending" }
Started request…
Received response: 200
```

1. calling the `fetch()` API, and assigning the return value to `fetchPromise` variable.
2. immediately after, logging `fetchPromise` variable.
This should output: Promise {<state>: “pending” }, telling us that we have a `Promise` object, and it has a state whose value is “pending”.
3. passing a **handler function** into the Promise’s then() method. When (and if) the fetch operation succeds, the promise will call our **handler**, passing in a `Response` object, which contains the server’s response.

Note that `Started request…` is logged before we receive the response. Unlike a synchronous function, fetch() returns while the request is still going on (pending)

---

[**Summary**](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif)

```jsx
const a = () => console.log('first')
const b = () => setTimeout(() => console.log(second),1000)
const c = () => console.log('third')

b(); a(); c(); //first, third, second
```

This is the correct execution during the **event loop**.

1. `b()` returns a callback(setTimeout) which enters the **Web API**.
2. `a()` returns a console.log() → first
3. `c()` returns a console.log() → third
4. `setTimeout(…)` returns a console.log()

If we want to execute code after a snippet has been completed, we can avoid callback hell by using `**Promise**` constructor that receives a callback.

```jsx
const a = () => {
	return new Promise (function(resolve) {
		console.log('First'); resolve()})
	}
const b = () => {
	return new Promise (function(resolve) {
		setTimeout(() => {console.log("Second"); resolve()}, 2000)})
	}
const c = () => console.log("Third");

b().then(a).then(c); //second, first, third
// or using Async:
const callChain = async () => {
	a();
	await b(); //execution stops here, waiting for resolve/reject
	c()};
callChain(); //first, second, third
```