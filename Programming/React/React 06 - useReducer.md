Created: April 12, 2023 12:29 PM
Status: Open
Updated: April 12, 2023 6:52 PM

## useReducer

**useReducer** is a React hook that provides an alternative way to **manage state** in a component. It’s similar to the `useState` hook but provides a more powerful way to manage complex state updates and logic.

---

Call `useReducer` at the top level of your component to manage its state with a *reducer*.

```tsx
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

useReducer accepts two values:

1. **reducer**: A function that specifies how the state gets updated. This function should take two arguments: a **state** and an **action**. The state argument is inferred by React when initializing the useReducer hook. You have to provide only the action when calling `dispatch`**.**
2. **initialArg**: This is the *initial state* value, which can be of any type.
3. **init**(optional): The initializer function that should return the *initial state*, result of **init(initialArg)**

useReducer returns two values:

1. **state**: It’s set to `initialArg` (or init(initialArg) if present)
2. **dispatch**: a function that invokes the `reducer` function. Accepts `action` as parameter.

---

The state is **never directly changed** (like useState)

but is returned from the reducer. **You can’t invoke the reducer** **directly**, but you’ll have to use `dispatch` instead.

`**dispatch**` accepts action as parameter (same of reducer).

You can **declare** the reducer function **outside** of your component.

### Nomenclature

**action** should have a method named `type` which should indicate the action to perform. It’s paired with the use of **switch-case**.

```tsx
function counterReducer(state, action) {
  switch (action.type) {
    case 'increment':
      return state + 1;
    case 'decrement':
      return state - 1;
    default:
      throw new Error('Unsupported action type');
  }
}

const Counter() => {
  const [count, dispatch] = useReducer(counterReducer, 0);

  function handleIncrement() {
    dispatch({ type: 'increment' });
  }

  function handleDecrement() {
    dispatch({ type: 'decrement' });
  }
```

**Remember** **that the case should always return**, otherwise the switch will pass to the next case, bringing unexpected behaviors.

---

<aside>
💡

</aside>

 Something

---