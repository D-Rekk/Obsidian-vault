Created: March 30, 2023 11:11 AM
Status: Open
Updated: March 30, 2023 11:40 AM

## Custom Hooks

Custom hooks are a great manner to reduce the clutter of your code, improving clarity and reusability. A **custom hook** is a function that returns other functions or variables into an object/array. 

A Custom Hook has following features:

- Its name starts with `**use**` like `useQuery`, `useMedia`…
- Unlike functional components, custom hooks return a normal, non-JSX data.
- Unlike other functions, custom hooks can use other hooks such as `useState`, `useRef` and other custom hooks.

*Custom hooks* are a great choice for separating **logic** from **UI**. They are reusable in many different components, hide complex logic within a component and make the code easier to read.

```tsx
export const useCustomHook = () => {
  const [count, setCount] = useState<number>(0);
  const incrementCount = (): void => {
    setCount((prevState) => prevState + 1);
  };
// you can also use arrayDestructuring with Ts
// return [count, incrementCount] as const;
  return { count, incrementCount };
};
//App.tsx
import {useCustomHook} from "./useCustomHook"
const {count, incrementCount} = useCustomHook
...
```

In this case, the main component only needed the `count` state and `incrementCount` function. Those

---