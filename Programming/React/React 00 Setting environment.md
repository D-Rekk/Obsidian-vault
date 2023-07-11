# React 00. Setting environment

Created: August 1, 2022 10:45 AM
Status: Open
Updated: August 16, 2022 4:38 PM

## Create React App

It is the most popular way to try out React and build a new single-page, client-side application. It’s made for React but isn’t opinionated about routing or data fetching.First, install [Node.js](https://nodejs.org/en/). Then open your terminal and run this line to create a project:

```bash
npx create-react-app my-app
cd my-project
```

---

### Add Tailwind CSS

Install **`tailwindcss`** and its peer dependencies via npm, and then run the init command to generate both **`tailwind.config.js`** and **`postcss.config.js`:**

```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Add the paths to all of your template files in your **`tailwind.config.js`** file:

```jsx
module.exports = {
  content: [
    "./src/**/*.{js,jsx,ts,tsx}",
  ], …
```

Then add the **`@tailwind`** directives to your **`./src/index.css`** file.

```jsx
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Run your build process with **`npm run start`**.

---

## Rendering Methods

### CSR. Client Side Rendering

Using **`create-react-app`** creates a JavaScript file that is going to be rendered as HTML. During the HTTP request, **the client is not going to see your website** until the Javascript is loaded. The SEO is not going to index your application because **the initial state of DOM is empty**. 

Great for **dynamic** single-page-applications, allowing us to reuse UI components across our application, without requesting them again from the server.

---

### SSR. Server Side Rendering

The server build-out the whole HTML file for you and send it to the browser. While browser renders the DOM, the Javascript files are being downloaded and executed in the background. The content can be fetched, rendered, and then sent to the client.
*This process is known as **hydration**.*

The downside are the creation of multiple HTML files on more pages of the application, making the navigation between pages quite slow.

---

### SSG. Static Side Generation

SSG describes the process of building websites that render **at build time**. The server is going to create all HTML files, assets such as JavaScript and CSS, and a few other static files. The page is pre-rendered at compile time. That means that the user won’t have to wait for the page to load at the browser.

The main difference between SSG and SSR is that **Static Side Generation** generates HTML **during build time**. This is a double-edged sword. The web application is going to be extremely fast, but the application is not going to be dynamic since, when a change is made, the website needs to rebuild and reload. This approach is **serverless**.

---

> When you create a react app using npx-create-react-app, you get a react app that doesn't support SSR or SSG which are good for SEO. Using npx create-next-app lets you choose between the SSR or SSG.
> 
