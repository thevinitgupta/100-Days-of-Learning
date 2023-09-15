# Discover Bun - A Faster, Modern JavaScript Runtime

<img src="https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/16e0a1d0-4e5e-46a2-9f6d-6be7e2b22b1b"/>

## Bun is the new Javascript Runtime built from scratch to serve the modern Javascript ecosystem.

But do we really need more Javascript tools?

<img src="https://media.giphy.com/media/d2lcHJTG5Tscg/giphy.gif"/>

Well, the Javascript Space is completely different from 15 years ago when NodeJS was first released.

- Yearly new releases of `ECMAScript`.
- Typescript becoming the norm because of the enhanced Developer experience.
- Use of JSX in almost every development framework.

These have forced the Javascript runtimes to become `lighter` and `faster`.

## Deno - Modern runtime that becamse Jurasic
A little bit ago, we got Deno. While it is just No-De reversed as De-No, it does more than that.

It's features are listed on their website : 

![Deno Features](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tx3clsz1vuiq2a8bg362.png)

But, Deno essentially failed, because : 

> Deno only really sported "minor features" from a users perspective. It had a cleaner codebase, used up-to-date best-practices, and had better security, but those things are really only "features" to a user, not a product in themselves.

## The Technology Behind Bun
Bun is a Javascript Runtime. But what does it mean actually?
It starts with an Engine - The Component of a runtime that runs the Javascript code. 

We all know V8, the JS Engine behind Chrome and NodeJS.
But Bun uses something different - `JavascriptCore`.

### Javascript Core is a `Performance🚀 focused` solution built by Apple 🍎 for the Safari Browser

The JS engine cannot work on it's own. So it combines with external APIs and message Queues and the infamous Event loop to create a Javascript Runtime.

![Javscript Runtime Internal working](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vqnm77ue4jdejhklnk7x.png)

In Bun, this is implemented from scratch using `Zig` which is a `low-level` general purpose language like C or Rust for building fast applications. 

### The above implementation provides better performance and memory management during Start and Runtimes, combined with the promise of mind-blowing speed, you have a real competitor of NodeJS.

![Bun Meme](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6p0e0cy5tdvz3dv6je9h.jpg)

## Features of Bun
Bun has a lot of great features that makes it worthy.
### 1. Support for NodeJS packages 🎯
Bun is like a Drop-In replacement for NodeJS thanks to the native implementation of 100s of Node modules

Bun also uses the `package.json` file for dependencies, so less learning curve from NodeJS and `bun install` is really fast 👇

![Bun speed](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zeq16xccepmdt9650fhd.png)

### 2. Built in Typescript Support and it's fast ⚡
Before the dawn of Bun, running typescript was tedious and slow. Bun comes with built in support for running Typescript in your projects and makes it faster. 

![Typescript Bun](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/s2w501y62psor9ox6wdt.png)

### 3. Support for both CommonJS and ESModules(MyFavorite) 🎉
Remember those days where you had to convert your project from the old `require` syntax to `import` syntax? Some libraries still not support the import syntax perfectly with Typescript. 

This all goes away with Bun. You can write either or both.

![Bun Features](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/86m8z894k6suwc876cy1.png)

### 4. Built-In Testing Support 💡
You love the Test driven development? Or are you just starting with it? It doesn't matter. Because you do not have to go and learn a new testing framework to do the job. 

Bun comes with built-in testing support, and so it is much faster from the other ones out there.

![Bun testing Benchmarks](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bgi5m2ywckerlag3yuk9.png)

#### Enough talk, let's see some examples of using Bun 📌
## Installing Bun
Installing Bun is as simple as below : 
```shell
curl -fsSL https://bun.sh/install | bash
```

## Setting up a Server
Ready to develop your own service? Create a new file : `server.ts` and add the following code : 

![Bun HTTP Server](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cptbnrm0fzbohr3ziddo.png)

## Start the server
Now to start listening to requests, run the following command(no intermediate step of converting to `.js` separately) : 
```shell
bun index.tsx
```

## React Components with Bun
Bun supports .jsx and .tsx files out of the box. Bun's internal transpiler converts JSX syntax into vanilla JavaScript before execution.

![JSX With Bun](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bj77oc2k00qcpbi186o1.png)
It also works with the above React component.

With the above features and many more, Bun is ready to become the new norm in the Javascript runtime market.

Do you want to use Bun in your projects? Checkout their official website for Getting Started and installation guides here : [Bun.js](https://bun.sh/)
