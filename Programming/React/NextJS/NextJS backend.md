> **Title**: NextJS backend
> **Date**: 2023/ 25th Jul
> **Tags**: #React #Typescript #NextJS #MongoDB #Prisma #mongoose
---
# Data Fetching
Since **Next.js 12** there has been the introduction of the *API Middleware*. These functions allow you to run code before the request is completed. Together with the *server components*, this allows a fast fetching on the server.
___
### server-side fetching
In the **server components** you can include an *async function* that will retrieve the data on the server before the component has loaded in the client.
```TS
const getPosts = async (): Promise<Post[]> => {
  const data = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await data.json();

  return posts;
};

export default async function Posts() {
  const posts = await getPosts();
  console.log(posts);

  return (
    <div className={inter.className}>
      <h1>Posts</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
---
### client-side fetching
In the **client components** the official documentation suggests to use *SWR* or *React Query* to handle the data fetching. Yet React introduced a way to accept async hooks inside components: it's the `use` hook built conceptually like await, but without type errors.
```TS
"use client"
const getPosts = async (): Promise<Post[]> => {
  const data = await fetch("https://jsonplaceholder.typicode.com/posts");
  const posts = await data.json();

  return posts;
};

export default function ClientPosts() {
  const posts = use(getPosts());

  return (
    <div className={inter.className}>
      <h1>Posts</h1>
      <ul>
        {posts.map((post) => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```
---


