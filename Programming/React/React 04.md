# React 04

Created: February 1, 2023 11:53 AM
Status: Open
Updated: February 1, 2023 1:47 PM

# React Router

**React Router** is a client and server-side routing library. It achieves a more seamless Ux experience by allowing the user to navigate through the app without the need for a full page reload.

**Routing** is the *mechanism by which page requests are redirected to the component* or code that handles them. Basically, it’s how React knows what UI components to present based on the route. This process improves the performance of the app and makes it more SEO friendly by using **SSR**(server-side rendering).

---

## Create a Routing app in React

First, you’ll need to install the `react-router-dom` dependency in your project. Then you’ll need to import the `BrowserRouter`, `Route`, and `Link`  ****components from `react-router-dom` ****in your **main.tsx** file.

```tsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter, Route, Routes } from "react-router-dom";
```

Our entry point is the **Browser Router** component. It basically consists of an interface that enables the React Router to run in the web browser. This is a new features that *“stores the current location in the browser's address bar using clean URLs and navigates using the browser's built-in history stack”*.

This component will be wrapping our entire Application

```tsx
ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
);
```

---

## Routes

A **route** is nothing more than a path that React Router will use to determine what component to render. The convention is usually to keep your routes components in **src/routes**. Let’s create the first route named **project.tsx.**

```tsx
const Project = () => {
  return <h2>This is the Project page 🧑‍💻</h2>;
};

export default Project;
```

---

Inside our **src/main.tsx** we can import the route and render it inside `element` prop of `<Route/>`.

```tsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<App />} />
    <Route path="project" element={<Project />} />
    <Route path="about" element={<About />} />
    <Route path="contact" element={<Contact />} />
  </Routes>
</BrowserRouter>
```

## Links & Navigation

`<Link/>` is a component imported from the `react-router-dom` that allows you to navigate from one route to another. It really similar to the HTML `<a>` tag.

Create a new component named **src/components/Nav/Navigation.tsx**. Export if through **.[.Nav/index.tsx](https://www.joshwcomeau.com/react/file-structure/)**.

```tsx
import { Link } from "react-router-dom";

const Navigation = () => (
  <>
    <nav className="navbar">
      <Link to="/">Home</Link>
      <Link to="/project">Projects</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  </>
);

export { Navigation };
```

```tsx
export * from "./Navigation";
export { Navigation } from "./Navigation";
```

---

Import the component in **src/App.tsx**

```tsx
import { Outlet } from "react-router-dom";
import { Navigation } from "./components/Navigation";

export default const App = () => (
  <div className="App">

	    <div className="Nav-bar">
		      <h1>Navbar</h1>
		      <header className="App-header">
		        <Navigation />
		      </header>
	    </div>
	    <div className="Routed">
		      <main className="App-content">
		        <Outlet />
		      </main>
	    </div>

  </div>
);
```

In the real world, we want to have a laout shared across most of the routes. This common layout is usually composed of one or more UI components, such as nav menu, header, footer, logo etc.

The newer version of **React Router**(6.0.3) introduced a new way of sharing layouts. The concept is called **Layout Routes** and consists of nested routes being rendered in a parent route.

Inside the parent we use the `Outlet` component from `react-router-dom` which behaves similar to `props.children` but it’s designed to render the children `route`s.

---

What if we want to render something in that Outlet space when the parent route itself is requested? This is where the **index** **method** comes in.

When to use `index` :

- Index routes are the default child route for a parent route.
- Index routes match when a parent route matches but none of the other children match (never happening with **catch-all route ***)
- Index routes render when the user hasn't clicked one of the items in a navigation list yet.

```tsx
<Route path="/" element={<App />}>
          <Route index element={<Home />} />
          <Route path="project" element={<Project />} />
          <Route path="about" element={<About />} />
          <Route path="contact" element={<Contact />} />
          <Route path="users" element={<Users />}>
            <Route path=":userID" element={<User />} />
          </Route>
          <Route path="*" element={<NotFound />} />
        </Route>
```