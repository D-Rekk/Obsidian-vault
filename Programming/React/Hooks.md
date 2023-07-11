
# Hooks

> **Hooks** are a quite recent addition to React. They let you use state and other features without writing a **class**. We can’t call hooks inside logical operations, loops nor nested functions. This allows to call hooks **in the same order** every component renders.

## useState

The first type of Hook is called **State Hook**. It is used to create and update local state in functional component. We need to import the **useState** hook, that will allow to create local state.

```jsx
import {useState} from 'react';
```

useState returns an **array** containing 2 values: `state` and `setState` .
The first argument **state** returns the same value passed as the first argument (our `initiaValue`). 

```jsx
const [state, setState] = useState(initialValue)
//Without destructuring:
const array = useState(initialValue)
const state = array[0]      //initialValue
const setState = array[1]   //function
```

The second value of the array **setState** is a function that allows us to update the properties of `state`. The function will receive the previous value of `state`, and return an updated value.

```jsx
setState(state + 1) // output: 2 with initial initialValue being 1
setState(state + 1) // output: 3
```

> `setState` cannot be invoked at **top-level**. It should be passed inside a **handler** **function**.
> 

---
## useEffect

The second type is called is **Effect Hook**, which is used to perform side effect in a function component **after it is rendered** to the DOM.

```jsx
import React, {useState,useEffect} from 'react';

function Example(){
	const [count, setCount] = useState(0):
	
	useEffect(() => {
		document.title = `You clicked me ${count} times`;
	});
	return(<>
		<p>You clicked {count} times</p>
		<button onClick={() => setCount(count+1)}></button>
		</>
	);
}
```

By using this Hook, React will remember the function you passed (we’ll refer to it as our ‘*effect*’ ) and **call it later** after performing the DOM updates.

Calling the `useEffect` inside a component we can access the `count` state variable (or any props) right from the *effect*. We don’t need any special API (build-in function) to read it. 

> **useEffect()** run after every render, by default. It runs both after the first render and after every update.

You might notice that the function passed to useEffect **is going to be different on every render**. This is intentional, since this is what lets us read the `count` value from inside the *effect* without worrying about it getting stale(becoming obsolete).

Every time we re-render, we schedule a *different effect*, replacing the previous one. This makes the effects behave more like a part of the render result - **each effect ‘belongs’ to a particular render**.