Created: May 26, 2022 10:48 PM
Status: Open
Updated: February 9, 2023 1:37 PM+
Tags: [[React 05 - Custom Hooks]]

# React 01

## Why use ReactJS

Many web interfaces are created with React. Its speciality is that React is *composable*. With modern frameworks we can take chunks of code and put it into our own custom components to assemble a larger webpage (in the past every element had to be its separate webpage).

**Maintanable** and **Flexibility** are the key words of using frameworks

---

## Code a React App

To build a static version of your app that renders your data model, you’ll want to build **components** that reuse other components and pass data using **props**.

Props (short for Properties) are a way of passing data from parent to child *in static pages* (**state** is similar, but used for interactivity, that is, changing data).

The common hierarchy for small pages is “**top down**”, while on larger projects is easier to go “**bottom-up**”.

---

## Components

The main files in our React App are: **`public/index.html`**, **`App.js`** & **`index.js`**. **App.js** is where our main component is going to be developed.

A **component** is a reusable function (or class) that **returns a React element**. These functional component accept props as argument and returns a building block. The special thing about functional components is that they don’t have access to *life cycle methods* (unless you use modern React hooks).

> **Life cycle methods** are a series of events that happen between initialization and the unmounting/destruction of the function itself
> 

---

The best practice to write functional components is a **function expression** rather than a declaration

```jsx
function App () { …
```

```jsx
const App = () => {…
```

We can use normal JavaScript before the **explicit** **return** statement. If the return is **implicit**, our use of JavaScript is going to be very limited.

---

[[Hooks]]
---

### Event Handlers

When using React, you generally don’t need to call `addEventListener` to add listeners to a DOM element after it is created. Instead, just provide a **listener** when the element is initially rendered. 

**Event handlers** are your own **functions** that will be triggered in response to user interactions like clicking, hovering, focusing on form inputs and so on.

To add an event handler, you first define a function and then pass it as a **prop** to the appropiate JSX tag.

```jsx
function handleClick() = {alert('You clicked me!')}
<button onClick={handleClick}>Click me</button>

```

> By convention, it is common to name event handlers as *handle* followed by the event name. You’ll often see `onClick={**handleClick**}`, `onMouseEnter={**handleMouseEnter**}` and so on.
> 

---

Functions passed to event handlers must be **passed**, not **called**.

```jsx
<button onClick={handleClick}>
```

```jsx
<button onClick={handleClick()}>
```

In the first example, the `handleClick` function is passed as an `onClick` event handler. This tells React to remember it and only call your function when the user click the button.

In the second example, the `()` at the end of `handleClick()` fires the function immediately during rendering, without any clicks. This is because JavaScript inside the JSX`{…}` executes right away.

---

### Keys

A “**key**” is a special string attribute you need to include **when creating lists of elements**. The **key** prop is used internally by React for performance reasons. It helps the library make sure to only re-render the array elements that have changed.

 >Keys should be given to the elements inside the array to give the elements stable identity (like IDs in HTML tags).

It’s **not recommend** using indexes for keys if the order of items may change. This can negatively impact performance and may cause issues with component state.

Keys only make sense in the context of the surrounding array. If you extract a `ListItem` component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` elements inside the list.

> Keys used withing arrays should be unique among their siblings. However, they don’t need to be globally unique. **We can use the same keys when we produce two different arrays**.

```jsx
function Blog(props) {
	const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
	const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
	);
}
```

---
![[ECMAScript 6#Props Destructuring]]

---

By the time we get to this **Listing** functional component, we already know we’re referencing a listing, so `props.listing` looks and feels redundant:

```jsx
const Listing = (props) => (
  <div>
    <p>Title: {props.listing.title}</p>
    <p>Type: {props.listing.type}</p> 
    <p>Location:
      {props.listing.location.city},
      {props.listing.location.state},
      {props.listing.location.country}
    </p>
  </div>
);
```

This block can be made to look much cleaner through destructuring. We can achieve this in the function parameter as **we pass the props in the argument**.

```jsx
const Listing = ({ listing }) => (
	<div>
	  <p>Title: {listing.title} </p>
	  <p>Type: {listing.type}</p>
	  <p>Location: 
		  {listing.location.city},
		  {listing.location.state},
		  {listing.location.country}
	  </p>
	</div>
);
```

Our **props parameter** can be further destructured with nested objects like:

```jsx
const Listing = ({
  listing: {
    title,
    type,
    location:{city,state,country}
  }
}) => (
  <div>
    <p>Title: {title}</p>
    <p>Type: {type}</p>
    <p>Location: {city}, {state}, {country}</p>
  </div>
);
```

A common mistake is destructuring only the keys like below and trying to access the parent object:

```jsx
const Listing = ({ location: {city, state, country })
```

In this scenario, *we wouldn’t be able to access the location object* through a variable named `location`. In order to do so, we’d have to **define it** first like so:

```jsx
const Listing = ({ location, location: {city, state, country })
```
