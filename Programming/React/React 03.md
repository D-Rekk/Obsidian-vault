# React 03

Created: September 27, 2022 11:43 AM
Status: Open
Updated: September 27, 2022 7:13 PM
Tags: ![[]]

## useEffect

The **useEffect API** is a React hook that allows you to run some custom code *after React renders* (or re-renders) a component to the DOM. It accepts a callback function that will be called after the component has been updated.

---

`**useEffect**` is useful to interact with **async data**, like **useState** hooks or **HTTP** requests.

```jsx
useEffect(() => {
	//your custom code;
},[]);
```

## useRef

The **useRef API** is a particular hook used to create some persisted mutable values, as well as access DOM Elements (HTML tags properties).

---

It accepts a single variable as **initialState** and return a **reference**(also **ref**).

```jsx
import { useRef } from 'react';
function MyComponent() {
  const reference = useRef(someValue);
  const someHandler = () => {
    const value = reference.current; // Access reference someValue:
    reference.current = newValue; // Update reference value:
  };
}
```

**`reference.current`** lets you access to your ref value. 

> **2 rules to remember about references:**
> 
> 1. The value of the reference is *persisted* (stays the same) between component re-renderings;
> 2. Updating a reference *doesn't trigger a component re-rendering*.

## useState vs useRef

**useState** is an *asynchronous call API*(even though you can’t await for it since it returns null). It is used mainly for *dynamic DOM elements* since it can **re-render** the components.

**useRef** is a synchronous hook. It is used to *perform logical stuff* since it **cannot re-render** a component. It is mostly used for DOM elements e.g. `Input` element, since access to `**current.value**` of the same and change it without performing a re-render(which happens at every digit if used with `useState`).

```jsx
const [isFlipping, setIsFlipping] = useState(false);

  let flipInterval = useRef<ReturnType<typeof setInterval>>();
	const startAnimation = () => {
    flipInterval.current = setInterval(() => {  //setInterval returns an ID
      setIsFlipping((prevFlipping) => !prevFlipping); //isFlipping becomes true
    }, 10000);
  };

  useEffect(() => {
    startAnimation();
    return () => flipInterval.current && clearInterval(flipInterval.current);
  }, []);

```

---