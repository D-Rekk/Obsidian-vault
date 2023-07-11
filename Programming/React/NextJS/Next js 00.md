Created: August 24, 2022 12:45 PM
Status: Open
Updated: August 24, 2022 1:42 PM

## What is Next.js

**Next.js** is a framework that was created by Vercel creator, Guillermo Rauch. Next.js allows to bring CRA to the back-end, making it the whole service by solving a lot of the problems created by CRA.

> It runs your React code on the back-end so you don’t have to worry about the SEO of your web-app. It actually renders the html with the basic content needed (SSR).
> 

The interesting way about how Next.js manages their packages is by handling it in the Next.js package directly. During the build it **will pull specific version of the packages it needs and bundle it into Next**, no as a sub-dependency through node but as an actual compiled file so you don’t have to manage the dependency. ***It just works*** 

The `**package.json**` and **`package-lock.json`** are surprisingly smaller than then CRA version, even though the implementation used as compared to the latter.

---
