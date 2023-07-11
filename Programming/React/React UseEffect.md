# React UseEffect

Created: November 7, 2022 12:37 PM
Status: Open
Updated: December 30, 2022 8:23 PM

### useEffect is not a lifecycle hook.
Its purpose is side effects

- **Lifecycle are a group of methods that belong to [class components](https://retool.com/blog/the-react-lifecycle-methods-and-hooks-explained/#:~:text=A%20React%20component%20undergoes%20three%20phases%20in%20its%20lifecycle%3A%20mounting,often%20called%20%E2%80%9Cinitial%20render.%E2%80%9D)**
    
    If you add dependencies in the dependency array, the function passed into the `useEffect` hook will run every time the dependencies, like a piece of stateful data, changes. This behavior of the `useEffect` hook is comparable to the `componentDidUpdate` method since it’s invoked on every state/props change. The difference is that you can specifically choose what state/props you want `useEffect` to depend on, rather than the `componentDidUpdate` which acts upon every `state` or props change.
    º

---

### It also is not a state setter.
It allows to synchronize React with external system

Use it to synchronize React with network, subscription, DOM.
Utilize useState or useContext, or a state-management API for state setter.

---

### Where do effects go?
Outside of the component

Since React 18, **strict mode** is going to mount the component, simulate the unmount(cleanup), then remount the component.

since **React 16.8 ≥**

```jsx
const Component = (props) => {
	useEffect(() =>{
		return () => {…}
	}, [/*...*/])

	return ( <div> {/*...*/}</div>)
}
```

from **React 18**

```jsx
useEffect(() =>{
	return () => {…}
}, [/*...*/])

const Component = (props) => {
	return ( <div> {/*...*/}</div>)
}
```

---

There’s mainly two types of effects
**Action effects** and **Activity effects**. Effects happen *outside* of rendering.

### State changes ⇒ update UI (DOM)
UI is a function of state

**[ state, event ] ⇒ nextState**

Given a state, and an event, trigger the next-state. This paradigm though leaves no room for effects.

### When do effect happen?
State transitions. Always.

Your state changes should happen for a reason and that reason **should not be** another state change. It should be an **action (effect)**.

******************************************Effects are state management
[ state, event ] ⇒ [nextState, effects]**

```jsx
function Component() {
	const [data, setData] = useState(null);
	useEffect(() => {
		let cancelled = false; //flag to cancel
		fetch(`some/resources`).then(data => {
			if (cancelled) return; 
			setData(data)
		}
		return () => {cancelled = true} //unmount
	},[]);
}
```

---

### How execute effects when handling events without useEffect?

```jsx
import {useState, useCallback} from 'react';
function useSpicyReduces(reducer, initialState, executeEffect){
	const spicyDispatch = useCallback((e) => {

		// Calculate next state
		const nextState = reducer(state, e);

		// Execute effect based on transition
		executeEffect(state, e, nextState);

		// Commit next state
		setState(nextState);
	};
	return (state, spicyDispatch);
	)
}
```

---

### Fetching data on render (is a lie)
Render-as-you-fetch with Suspense

You’re going to find that event-handler, start fetching in there, repack in your component and make use of **Suspense** or an external library (useSWR & **useQuery**) (or use **Remix/Next.js**)

### **useEffect is synchronization
State transitions trigger effects
Effects go in event-handlers**

Find the event-handler that triggers your effect and put the effect in there.

---

```jsx
import { useState, useEffect } from 'react';

function ExampleComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    let cancelled = false; // flag to cancel
    fetch('some/resources').then(data => {
      if (cancelled) return;
      setData(data)
    }
    return () => { cancelled = true } // unmount
  }, []);

  return (
    <div>
      {/* ... */}
    </div>
  )
}
```