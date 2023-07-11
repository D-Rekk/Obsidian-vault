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
