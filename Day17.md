# Building Lynkit - URL Shortener Day 1 : Setting up ExpressJS Server with Typescript
Lynkit will be a full stack URL shortener application built using `ReactJS, NodeJS, Typescript, MongoDB and Redis` for caching.

The first step is building the REST API using ExpressJS with Typescript and MongoDB.

## Setup for ExpressJS to use Typescript
 - Create a new folder and run : 
```js
npm init -y
```
This initialized an npm respository with default options. 

 - Next, step is to install the necessary dependencies to run Typescript.
> 📌 The dependencies needed for running Typescript will only be needed during development, so we will install them as `DevDependencies` using the following command :
> ```js
> npm install -D typescript nodemon ts-node
> ```

When these are installed, we need to configure the environment.

- Next, we need to configure typescript, so create a new file : `tsconfig.json` in the root directory and add the following :
  ```js
  {
    "compilerOptions" : {
        "module": "Node16",
        "moduleResolution": "node",
        "baseUrl": "src",
        "outDir": "dist",
        "sourceMap": true,
        "noImplicitAny": true
    },
    "include": ["src/**/*"]
  }
```
